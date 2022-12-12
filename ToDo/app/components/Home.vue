<template>
    <Page>
        <ActionBar>
            <Label text="ToDo"/>
        </ActionBar>
        <StackLayout class="stack4">
            <FlexboxLayout>
                <StackLayout class="stack">
                    <template v-if="falseCounter() > 0 || trueCounter() > 0">
                        <FlexboxLayout class="flex1" v-for="Task, index in Tasks" :key = "index" v-if="Task.status === false  && itemDisabled === false" >
                            <StackLayout class="stack1">
                                <Button text = "✔️" @tap = "IsDone(Task,index)"  />
                            </StackLayout>
                            <StackLayout class="stack2">
                                <Label class="label">{{Task.NewTitle}}</Label>
                                <TextView class="Tview" editable="false"> {{Task.NewDesc}} </TextView>
                            </StackLayout>
                            <StackLayout class="stack3">
                                <Button text = "➖" @tap = "DeleteTask(index)"  />
                                <Button text = "✏️" @tap = "EditTask(index,Task)" />
                            </StackLayout>
                        </FlexboxLayout>
                    </template>
                    <label class="label" v-if="falseCounter() === 0 && itemDisabled === false">Нет запланированных задач</label>
                    <template v-if="falseCounter() > 0 || trueCounter() > 0">
                        <FlexboxLayout class="flex1" v-for="Task, index in Tasks" :key = "index" v-if="Task.status === true  && itemDisabled === true" >
                            <StackLayout class="stack1">
                                <Button text = "✖️" @tap = "IsDone(Task,index)"  />
                            </StackLayout>
                            <StackLayout class="stack2">
                                <Label class="label">{{Task.NewTitle}}</Label>
                                <TextView class="Tview" editable="false"> {{Task.NewDesc}} </TextView>
                            </StackLayout>
                            <StackLayout class="stack3">
                                <Button text = "➖" @tap = "DeleteTask(index)"  />
                                <Button text = "✏️" @tap = "EditTask(index,Task)" />
                            </StackLayout>
                        </FlexboxLayout>
                    </template>
                    <label class="label" v-if="trueCounter() === 0 && itemDisabled === true">Нет выполненных задач</label>
                </StackLayout>
                <FlexboxLayout class="flex">
                    <Switch v-model = "itemDisabled"/>
                    <Button text = "➕" class="btn" @tap = "$navigateTo(CreatePage)" />
                </FlexboxLayout>
            </FlexboxLayout>
        </StackLayout>
    </Page>
</template>

<script>
import NewTodo from './ToDoCreate.vue'
import { ApplicationSettings } from '@nativescript/core';

  export default {
    data() {
        return {
            itemDisabled: false,
            CreatePage: NewTodo,
            Tasks: JSON.parse(ApplicationSettings.getString("TaskDb")),
            Db:[]
        };
    },
    props:{
        variables: Object,
        variablesEdited: Object,
        IndexEdited: Number
    },
    methods:{
        IsDone(Task,index)
        {
            if(Task.status === false)
            {
                Task.status = true
            }
            else
            {
                Task.status = false
            }
            this.Db = JSON.parse(ApplicationSettings.getString("TaskDb"))
            this.Db.splice(index,1,Task)
            ApplicationSettings.setString("TaskDb", JSON.stringify(this.Db));
            this.Tasks = JSON.parse(ApplicationSettings.getString("TaskDb"))
        },
        AddTask()
        {
            this.Db = JSON.parse(ApplicationSettings.getString("TaskDb"))
            this.Db.push(this.variables);
            ApplicationSettings.setString("TaskDb", JSON.stringify(this.Db));
        },
        DeleteTask(index)
        {
            confirm('Удалить задачу?')
                .then(result => {
                    if(result){
                        this.Db = JSON.parse(ApplicationSettings.getString("TaskDb"))
                        this.Db.splice(index, 1)
                        ApplicationSettings.setString("TaskDb", JSON.stringify(this.Db));
                        this.Tasks = JSON.parse(ApplicationSettings.getString("TaskDb"))
                    }
                });
        },
        EditTask(index,Task)
        {
            this.$navigateTo(NewTodo,
                {
                    props:{
                        TaskToChange:{
                        },
                        status: Task.status,
                        index: index
                    }
                })
        },
        trueCounter()
        {
            let TrueCount = 0
            for (let i = 0; i <= this.Tasks.length -1; ++i)
            {
                if(this.Tasks[i].status === true)
                {
                    TrueCount++
                }
            }
            return TrueCount
        },
        falseCounter()
        {
            let FalseCount = 0
            for (let i = 0; i <= this.Tasks.length -1; ++i)
            {
                if(this.Tasks[i].status === false)
                {
                    FalseCount++
                }
            }
        return FalseCount
        }
    },
    mounted()
    { 
        console.log(typeof ApplicationSettings.getString("TaskDb"))
        if (typeof JSON.parse(ApplicationSettings.getString("TaskDb") === undefined))
        {
            ApplicationSettings.setString("TaskDb", JSON.stringify(this.Db));
        }
        console.log(ApplicationSettings.getString("TaskDb"))
        if(typeof this.variables != "undefined" )
        {
            this.AddTask()  
            this.Tasks = JSON.parse(ApplicationSettings.getString("TaskDb"))
            this.variables = ''
        }
        else if(typeof this.variablesEdited != "undefined" )
        {
            this.Db = JSON.parse(ApplicationSettings.getString("TaskDb"))
            this.Db.splice(this.IndexEdited,1,this.variablesEdited)
            ApplicationSettings.setString("TaskDb", JSON.stringify(this.Db));
            this.Tasks = JSON.parse(ApplicationSettings.getString("TaskDb"))
            this.variablesEdited = ''
        }
    },
};
</script>

<style>
label
{
    color: black;
}
.Tview
{
    font-size: 14px;
    color: white;
}
.btn
{
    background-color: blue;
    border-radius: 100%;
    width: 100px;
    height: 219px;
}
.label
{
    font-size: 15px;
    color: white;
}
.button1
{
    width: 20px;
    height: 20px;
}
.flex1
{
    width: 100%;
    border-color: #30c8f7;
    border-width: 2;
    box-sizing: border-box;
}
.stack4
{
    background-color: #212c30;
}
.stack1
{
    width: 200px;
}
.stack2
{
    width: 600px;
}
.stack3
{
    width: 200px;
}
    .stack
    {
        width: 1050px;
        height: 100%;
    }
    .flex
    {
        flex-direction: column;
        justify-content: space-between;
        height: 100%;
    }
</style>
