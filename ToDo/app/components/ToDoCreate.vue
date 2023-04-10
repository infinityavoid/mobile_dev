<template>
    <Page>
        <ActionBar>
            <Label v-if="status" text="Редактирование задачи"/>
            <Label v-else text="Создание задачи"/>
        </ActionBar>
        <StackLayout class="stack4">
                <StackLayout class="grid">
                    <label text = "Название задачи:" />
                    <TextField v-model = "TextFieldValue" hint = "Введите название..." />
                    <label text = "Описание:"/>
                    <TextView v-model = "TextViewValue" hint = "Введите описание..." textWrap="true"/>
                </StackLayout>
            <Button v-if="status" text="✔️" @tap = "Edited()" />
            <Button v-else text="✔️" @tap = "Completed()" />
        </StackLayout>
    </Page>
</template>

<script>
import Home from './Home.vue'
  export default {
    data() {
        return {
            TextFieldValue:'',
            TextViewValue:'',
            Task:[],
            Status: false
        };
    },
    props:{
        TaskToChange: Object,
        index: Number,
        status: Boolean
    },

    methods: {
        Edited()
        {
            if (this.TextFieldValue != '')
            {
                this.$navigateTo(Home,
                {
                    props:{
                        variablesEdited:{
                            NewTitle: this.TextFieldValue,
                            NewDesc: this.TextViewValue,
                            status: this.status
                        },
                        IndexEdited: this.index
                    }
                })
            }
            else
            {
                alert('Введите название')
            }
        },
        Completed() 
        {
            if (this.TextFieldValue != '')
            {
                this.status = false
                this.$navigateTo(Home,
                {
                    props:{
                        variables:{
                            NewTitle: this.TextFieldValue,
                            NewDesc: this.TextViewValue,
                            status: this.status
                        }
                    }
                })
            }
            else
            {
                alert('Введите название')
            }
        }
    },
    mounted()
    {
        if(typeof this.TaskToChange != "undefined")
        {
            this.status = true
            this.Task.push(this.TaskToChange)
        }
        else
        {
            this.status = false
        }
    }
};
</script>

<style>
label
{
    font-size: 15px;
    padding-top: 45%;
    padding-left: 5%;
    color: white;
}
.textv
{
    font-size: 15px;
    color: white;
}
.grid
{
 background-color: white;
 width: 100%;
 height: 1000px;
}
.stack4
{
    background-color: #212c30;
}
</style>
