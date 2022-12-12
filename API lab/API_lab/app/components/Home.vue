<template>
    <Page>
        <ActionBar>
            <Label text="NetWorking"/>
        </ActionBar>
        <StackLayout class="flexy" >
            <FlexboxLayout class="flexy" flexDirection="column">
                <button class="btn1" text = "Pokemons" @tap="$navigateTo(Pokemon)"/> 
                <button class="btn1" text = "Abilitys" @tap="$navigateTo(Ability)"/>
                <button class="btn1" text = "Items" @tap="$navigateTo(Items)"/> 
            </FlexboxLayout>
        </StackLayout>
    </Page>
</template>

<script>
import ItemsPage from './Items.vue'
import AbilityPage from './Ability.vue'
import PokemonPage from './Pokemon.vue'
  export default {
   data(){
    return{
        Items:ItemsPage,
        Ability:AbilityPage,
        Pokemon:PokemonPage,
    }
   }
    
  };
</script>

<style >
.flexy
{
    height: 100%;
    justify-content: space-between;
    background-color: gray;
}
.btn1
{
    width: 100px;
    height: 20%;
    border-radius: 50%;
    background-color: bisque;
}
</style>
