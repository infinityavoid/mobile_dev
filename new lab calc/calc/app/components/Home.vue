<template>
    <Page>
        <ActionBar>
            <Label text="Calculator"/>
        </ActionBar>

        <GridLayout columns="*, *, *, *" rows="*, *, *, *, *, *, *, *, *, *" class="grid">
            <TextField v-model="textFieldValue" row="0" col = "0" colSpan="4" rowSpan="5" class="textfield" editable = "false" label="Outlined" color = "#FFFFFF"/>
            <Button text="1" row = "5" col = "0" @tap="inputNum(1)" class = "buttonNum"/>
            <Button text="2" row = "5" col = "1" @tap="inputNum(2)" class = "buttonNum"/>
            <Button text="3" row = "5" col = "2" @tap="inputNum(3)" class = "buttonNum"/>
            <Button text="+" row = "5" col = "3" @tap="inputOp('+')" class = "buttonOp"/>
            <Button text="4" row = "6" col = "0" @tap="inputNum(4)" class = "buttonNum"/>
            <Button text="5" row = "6" col = "1" @tap="inputNum(5)" class = "buttonNum"/>
            <Button text="6" row = "6" col = "2" @tap="inputNum(6)" class = "buttonNum"/>
            <Button text="-" row = "6" col = "3" @tap="inputOp('-')" class = "buttonOp"/>
            <Button text="7" row = "7" col = "0" @tap="inputNum(7)" class = "buttonNum"/>
            <Button text="8" row = "7" col = "1" @tap="inputNum(8)" class = "buttonNum"/>
            <Button text="9" row = "7" col = "2" @tap="inputNum(9)" class = "buttonNum"/>
            <Button text="/" row = "7" col = "3" @tap="inputOp('/')" class = "buttonOp"/>
            <Button text="R" row = "9" col = "0" @tap="reset()" class = "buttonOp"/>
            <Button text="0" row = "8" col = "1" @tap="inputNum(0)" class = "buttonNum"/>
            <Button text="^x" row = "8" col = "2" @tap="inputOp('**')" class = "buttonOp"/>
            <Button text="*" row = "8" col = "3" @tap="inputOp('*')" class = "buttonOp"/>
            <Button text="√" row = "8" col = "0" @tap="Sqrt()" class = "buttonOp"/>
            <Button text="." row = "9" col = "1" @tap="inputOp('.')" class = "buttonOp"/>
            <Button text="=" row = "9" col = "2" @tap="calc()" colSpan = "2" class = "buttonOp"/>
        </GridLayout>

    </Page>
</template>

<script>
  export default {
    data()
    {
        return{
        NewNum: false,
        textFieldValue: '',
        PendingOp: false,
        }
    },
    methods: {
        inputNum: function(qetery)
        {
                this.textFieldValue = this.textFieldValue.toString();
                this.textFieldValue += qetery;
                this.NewNum = true;
                this.PendingOp = false;
        },
        inputOp: function(qetery)
        {
            if ((this.NewNum === true) && (this.PendingOp === false))
            {
                this.textFieldValue = this.textFieldValue.toString();
                this.textFieldValue += qetery;
                this.PendingOp = true;
            }
        },
        reset : function()
        {
            this.textFieldValue = '';
            this.NewNum = false;
            this.PendingOp = false;

        },
        calc: function()
        {
            if ((this.NewNum === true) && (this.PendingOp === false))
            {
                    /*if (isNaN(eval(this.textFieldValue).toString()) === true)
                    {
                        alert('Ошибка!');
                        this.textFieldValue = '';
                        this.NewNum = false;
                        this.PendingOp = false;
                        return;
                    }  
                    else if ( isFinite(eval(this.textFieldValue)) === false)
                    {
                        alert('Ошибка!');
                        this.textFieldValue = '';
                        this.NewNum = false;
                        this.PendingOp = false;
                        return;    
                    } 
                    else
                    {
                        this.textFieldValue = eval(this.textFieldValue).toString();
                    }*/
                    try
                    {
                        this.textFieldValue = eval(this.textFieldValue).toString();
                    }
                    catch
                    {
                        alert('Ошибка!');
                        this.textFieldValue = '';
                        this.NewNum = false;
                        this.PendingOp = false;
                    }
            }
        },
        /*delete_last: function()
        {
            this.textFieldValue = String(this.textFieldValue).slice(0,-1)
        }*/
        Sqrt()
        {
            if ((this.NewNum === true) && (this.PendingOp === false))
            {
                try
                {
                    this.textFieldValue = Math.sqrt(eval(this.textFieldValue).toString())
                }
                catch
                {
                    alert('Ошибка!');
                    this.textFieldValue = '';
                    this.NewNum = false;
                    this.PendingOp = false;
                }
            }
        }
    }
  };
</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';

    // Custom styles
    Button:active
    {
        background-color: #3c852a;
    }
    .fas {
        @include colorize($color: accent);
    }

    .info {
        font-size: 20;
        horizontal-align: center;
        vertical-align: center;
    }
    .grid
    {
        background-color: #000000;
        width: 100%;
        height: 100%;
    }
    .buttonNum
    {
        background-color: #FF8B00;
        
    }
    .buttonOp
    {
        background-color: #787878;//787878
    }
    .textfield
    {
        font-size: 20px;
        background-color: #000000;
        border-radius: 20%;
        padding-bottom: 800px;
        padding-left: 30px;
    }
</style>
