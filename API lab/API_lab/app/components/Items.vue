<template>
    <Page>
        <ActionBar>
            <Label text="Items"/>
        </ActionBar>
        <StackLayout>
            <FlexboxLayout class="flex1">
                <TextField class="text3" v-model = "TextFieldValue" hint = "Enter item name..."/>
                <button text = "🔍" @tap = "Get()"/>
            </FlexboxLayout>
            <template v-if="Name">
                <FlexboxLayout class="flex2" flexDirection="column">
                        <FlexboxLayout class="flex">
                            <label class="text">{{Name}}</label>
                        </FlexboxLayout>
                        <FlexboxLayout>
                            <label class="text2" editable="false">Effect: {{Effect}} </label>
                        </FlexboxLayout>
                        <FlexboxLayout>
                            <label class="text2" >Category: {{Category}} </label>
                        </FlexboxLayout>
                        <FlexboxLayout>
                            <label class="text2" >Cost: {{Cost}} </label>
                        </FlexboxLayout>
                </FlexboxLayout>
            </template>
            <button class="btn" text = "Back" @tap = "$navigateTo(Home)"/>
        </StackLayout>
    </Page>
</template>

<script>
import { Http } from '@nativescript/core'
import HomePage from './Home.vue'
  export default {
   data(){
    return{
    Home:HomePage  ,  
    TextFieldValue:'',
    Effect:'',
    Cost:'',
    Category:'',
    Name:''
    }
   },
   methods:
   {
    Get()
    {
        console.log('https://pokeapi.co/api/v2/item/' + this.TextFieldValue.toLowerCase().replace( /" "/g, "-" ))
        Http.getJSON('https://pokeapi.co/api/v2/item/' + this.TextFieldValue.toLowerCase().replace( /" "/g, "-" )
        ).then(
        (result) => {
        this.Cost = result.cost
        this.Sprite = result.sprites.default
        this.Effect = result.effect_entries[0].short_effect
        this.Category = result.category.name
        this.Name = this.TextFieldValue
    },
    )
    .catch(err => console.log(err))
    }

   },
  };
</script>

<style >

.btn
{
    align-self: flex-end;
}
.flex1
{
    border-color: #30c8f7;
    border-width: 2;
    box-sizing: border-box;
    justify-content: space-between;
}
.label
{
    font-size: 14px;
    text-align: center;
    align-items: center;
}
.label2
{
    font-size: 14px;
    height: 200px;
    width: 100%;
    text-align: center;
}
.stack2
{
align-items: center;
}
.text3
{
    font-size: 20px;
}
.text2
{
    font-size: 20px;
    width: 100%;
}
.flex
{
    
    justify-content: space-between;
}
.text
{
    flex: 1 1 auto;
    font-size: 35px;
}
.flex2
{
    justify-content: space-between;
    width: 100%;
    height: 50%;
}
</style>