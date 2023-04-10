<template>
    <Page>
        <ActionBar>
            <Label text="Converter"/>
        </ActionBar>
        <FlexboxLayout class="flex3">
            <Button @tap="$navigateTo(KgConverter)" class="btn1"/>
            <Button @tap="$navigateTo(LenghtConverter)" class="btn2"/>
            <Button @tap="$navigateTo(SecConverter)" class="btn3"/>
            <Button @tap="$navigateTo(RadConverter)" class="btn4"/>
            <Button @tap="$navigateTo(TemperatureConverter)" class="btn5"/>
            <Button @tap="$navigateTo(RenConverter)" class="btn6"/>
        </FlexboxLayout>
    </Page>
</template>

<script>

import kgGVue from './Weight/kg-fut.vue';
import Lenght from './Lenght.vue';
import Time from './SectoH.vue';
import Rad from './RadToGrad.vue';
import Temp from './Temperature/Temperature.vue';
import ZTR from './ZtoR.vue';


  export default {
    data()
    {
        return{ 
        KgConverter: kgGVue,
        LenghtConverter: Lenght,   
        SecConverter: Time,
        RadConverter: Rad,
        TemperatureConverter: Temp,
        RenConverter: ZTR,
        }
    }, 
   
   methods:{

   }
  };
</script>

<style >
.flex3
{
    align-items: center;
flex-wrap: wrap;
justify-content: space-around;
}

.btn1
{
    background-image: url("~/components/pngs/q.png");
    width: 30%;
    height: 30%;
    background-repeat: no-repeat;
    background-position: center;

}
.btn2
{   
    background-image: url("~/components/pngs/w.png");
    width: 30%;
    height: 30%;
    background-repeat: no-repeat;
    background-position: center;
}
.btn3
{
    background-image: url("~/components/pngs/e.png");
    width: 30%;
    height: 30%;
    background-repeat: no-repeat;
    background-position: center;
}
.btn4
{
    background-image: url("~/components/pngs/t.png");
    width: 30%;
    height: 30%;
    background-repeat: no-repeat;
    background-position: center;
}
.btn5
{
    background-image: url("~/components/pngs/r.png");
    width: 30%;
    height: 30%;
    background-repeat: no-repeat;
    background-position: center;
}
.btn6
{
    background-image: url("~/components/pngs/y.png");
    width: 30%;
    height: 30%;
    background-repeat: no-repeat;
    background-position: center;
}


</style>
