<template>
    <Page>
        <ActionBar>
            <Label text="Converter"/>
        </ActionBar>
    <StackLayout >
            <StackLayout backgroundColor="#d4d8d4">
                <FlexboxLayout>
                    <label > Из: </label>
                    <label  v-if = "status"> Часы </label>
                    <label  v-else> Секунды </label>
                </FlexboxLayout>
                <FlexboxLayout>
                    <label > В: </label>
                    <label  v-if = "status"> Секунды </label>
                    <label  v-else> Часы </label>
                </FlexboxLayout>
            </StackLayout>
            <FlexboxLayout >
                <TextField v-model = "textFieldValue"  hint="Введите значение..." editable = "false" class="textfield" />
                <Button class = "buttoninv" @tap="status = !status, Replace()" />
                <TextField v-model = "Changed" editable = "false" class="textfield2" />
            </FlexboxLayout>
        <FlexboxLayout backgroundColor="#d4d8d4" class="flex2">
            <FlexboxLayout class="flex1" >
                <Button v-for="button  in buttons"  @tap="Convert(button)" class = "buttonNum" > {{button}} </Button>
                <Button text="0" @tap="Convert('0')" class = "buttonNum"/>
                <Button text="." @tap="tochka('.')" class = "buttonNum"/>
            </FlexboxLayout>
            <FlexboxLayout  >
                <Button text="<-" @tap="delete_last()" class="buttonOp"/>
                <Button text="R" @tap="Reset()" class ="buttonOp"/>
            </FlexboxLayout>
        </FlexboxLayout>
        <Button text="Назад" class="btnback" @tap="$navigateTo(Home)" />
      </StackLayout>
    </Page>
</template>

<script>
import HomeVue from './Home.vue';

  export default {
    data()
    {
        return{
        Home: HomeVue,   
        sec: 3600,
        H: 3600,
        textFieldValue: '',
        Changed: '',
        status: true,
        buttons: ['1','2','3','4','5','6','7','8','9',],
        pos: '',
        }
    },   
   methods:{

    tochka: function(num)
    {
        if(String(this.textFieldValue[this.textFieldValue.length - 1]) != '.')
        {
            this.textFieldValue += num; 
        }
    },
    Reset: function()
    {
        this.textFieldValue = '',
        this.Changed = '';
    },
    delete_last: function()
    {
        if(this.textFieldValue != '')
        {
        this.textFieldValue = String(this.textFieldValue).slice(0,-1);

        }
    },

    Replace: function()
    {
        this.pos = this.textFieldValue; 
        this.textFieldValue = this.Changed;
        this.Changed = this.pos; 
    },

    Convert: function(num)
    {
        if(this.status == true)
            try
            {
                this.textFieldValue += num;
                this.Changed = this.textFieldValue * this.sec;
            }
            catch
            {
                alert('Данные введены не корректно')
            }
        else
        {
            try
            {
                this.textFieldValue += num;
                this.Changed = this.textFieldValue / this.H;
            }
            catch
            {
                alert('Данные введены не корректно')
            }
        }

    }

   }
  };
</script>

<style src="../mystyles.css">
 
</style>
