<template>
    <Page>
        <ActionBar>
            <Label text="Pokemon"/>
        </ActionBar>
        <StackLayout>
            <FlexboxLayout class="flex1">
                <TextField class="text2" v-model = "TextFieldValue" hint = "Enter pokemon name..."/>
                <button text = "🔍" @tap = "Get()"/>
            </FlexboxLayout>
            <template v-if="Name">
                <FlexboxLayout class="flex2" flexDirection="column">
                        <FlexboxLayout class="flex">
                            <label class="text">{{Name}}</label>
                            <Image :src="Sprite" stretch="none" />
                        </FlexboxLayout>
                        <FlexboxLayout class="wrap">
                            <Label class="text5" > Type: </Label>
                            <Label class="text3" v-for="Type in Types">{{Type.type.name}} </Label>
                        </FlexboxLayout>
                        <FlexboxLayout class="wrap">
                            <Label class="text4"> Ability: </Label>
                            <Label class="text3" v-for="Ability in Abilitys">{{Ability.ability.name}} </Label>
                        </FlexboxLayout >
                        <FlexboxLayout class="flex">
                            <StackLayout class="stack2" v-for="stat,i in Stats" :key = "i">
                                <label class="label">{{stat.base_stat}}</label>
                                <TextView class="label2" editable = "false">{{SName[i]}}</TextView>
                            </StackLayout>
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
    SName:['hp','attack','defense','special attack','special defense','speed'],
    TextFieldValue:'',
    Abilitys:'',
    Sprite:'',
    Types:'',
    Stats:'',
    Name:'',
    }
   },
   methods:
   {
    Get()
    {
        Http.getJSON('https://pokeapi.co/api/v2/pokemon/' + this.TextFieldValue.toLowerCase()
        ).then(
        (result) => {
        this.Abilitys = result.abilities
        this.Sprite = result.sprites.other['official-artwork'].front_default
        this.Types = result.types
        this.Stats = result.stats
        this.Name = this.TextFieldValue
    },
    )
    .catch(err => console.log(err))
    },
   },
  };
</script>

<style >
.wrap
{
    justify-content: flex-start;
}
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
    width: auto;
    font-size: 18px;

}
.text2
{
    font-size: 20px;
}
.text5
{
    width: 13%;
    font-size: 18px;
}
.text4
{
    width: 16%; 
    font-size: 18px;
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
    height: 50%;
}
</style>