<template>
    <Page>
        <ActionBar>
            <Label text="Ability"/>
        </ActionBar>
        <StackLayout>
            <FlexboxLayout class="flex1">
                <TextField class="text3" v-model = "TextFieldValue" hint = "Enter ability name..."/>
                <button text = "🔍" @tap = "Get()"/>
            </FlexboxLayout>
            <template v-if="Name">
                <FlexboxLayout class="flex">
                    <label class="text">{{Name}}</label>
                </FlexboxLayout>
                <FlexboxLayout class="flex2" flexDirection="column">
                    <TextView class="text2" editable="false">Effect: {{Effect}} </TextView>
                </FlexboxLayout>
                <FlexboxLayout class="flexi">
                    <Label class="text2"> Pokemons with this ability: </Label>
                    <label class="text2" v-for="pokemon in pokemons">{{pokemon.pokemon.name + ", "}}</label>
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
    Name:'',
    pokemons:''
    }
   },
   methods:
   {
    Get()
    {
        Http.getJSON('https://pokeapi.co/api/v2/ability/' + this.TextFieldValue.toLowerCase()
        ).then(
        (result) => {
        this.Effect = result.effect_entries[1].effect
        this.Name = this.TextFieldValue
        this.pokemons = result.pokemon
    },
    )
    .catch(err => console.log(err))
    }

   },
  };
</script>

<style >
.flexi
{
    flex-wrap: wrap;
}
.text4
{
    font-size: 15px;
    width: 100%;
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

.text3
{
    font-size: 20px;
    width: 100%;
}
.text2
{
    width: auto;
    height: auto;
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
    text-align: center;
}
.flex2
{
    width: 100%;
    height: 30%;
}

</style>