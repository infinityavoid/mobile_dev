<template>
    <Page>
        <ActionBar>
            <Label text="Home"/>
        </ActionBar>
        <StackLayout style="background: #F0F0F0">
            <StackLayout style="margin-top: 230px;">
                <label class="stack">{{Months.Name}}</label>
            </StackLayout>
            <StackLayout class="stack">
                <label>{{Months.Year}}</label>
            </StackLayout>
            <FlexboxLayout class="body">
                <StackLayout v-for="week, index in calendar.weeks" :key="index" class="week" >
                    <Label class="day" style="font-weight: 500">{{weekNames[index]}}</Label>
                    <StackLayout v-for="d, index in week" :key="index">
                        <Label :class="{'now-day': today(d, Months.Number)}" class="day">{{d}}</Label>
                    </StackLayout>
                </StackLayout>
            </FlexboxLayout>
            <FlexboxLayout class="btns">
                <Button text = "<-" @tap = "Back()" class="btn"/>
                <Button text = "back" @tap = "nowMonth()" class="btn"/>
                <Button text = "->" @tap = "Next()" class="btn" />
            </FlexboxLayout>
        </StackLayout>
    </Page>
</template>

<script>
  export default {
    data() {
        return {
            monthsNames: ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"],
            weekNames: ['Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб', 'Вс'],
            Days: ['1', '2', '3', '4', '5', '6', '0'],
            Data: new Date(),
            Months: {   
                Name: '', //название месяца
                Number: '', //номер месяца начиная с 0
                NOD: '', //кол-во дней в месяце
                Year: '' //год 
            },
            nowMon: '',
            calendar: {
                days: '',
                name: '',
                weekNames: '',
            }
        };
    },
    
    computed:{
    },
    methods:{
        initCal() 
        {
            this.Day = this.Data.getDate()
            this.Month = this.Data.getMonth()
            this.Year = this.Data.getFullYear()
            this.Months.Name = this.fnmonthday(this.Year,this.Month)
            this.Months.NOD = this.fnNOD(this.Year,this.Month)
            this.Months.Number = new Date(this.Year,this.Month).getMonth(),
            this.Months.Year = new Date(this.Year,this.Month,1).getFullYear()
            this.nowMon = new Date(this.Year,this.Month).getMonth()
        },
        today(day, numberMonth) 
        {
            if (day === this.Day && numberMonth === this.nowMon) 
            {
                return true
            }
            return false
        },
        calculatemd()
        {
            this.calendar = {}
            this.calendar = 
            {
                days: this.Months.NOD,
                name: this.Months.Name,
            }
            this.WeekDays()
            console.log(this.Months)

        },
        WeekDays()
        {
            let days = []
            let weeks = []
            let status = false
            for (let i = 0; i < 7; ++i) 
            {
                days = []
                for (let dd = 1; dd < i + 2; ++dd) 
                {
                    if (this.getDay(dd) == this.Days[i]) 
                    {
                        status = true
                        break
                    }
                    else {
                        if (status === false) 
                        {
                            days.push(' ')
                            break
                        }                    
                    }
                }
                for (let d = 1; d < this.Months.NOD + 1; ++d) 
                {
                    if (this.getDay(d) == this.Days[i]) {                       
                        days.push(d) 
                    }
                }
                weeks.push(days)
            }
            this.calendar.weeks = weeks
        },
        getDay(day)
        {
            let num = new Date(this.Months.Year,this.Months.Number,day).getDay()
            return num 
        },
        fnmonthday(y,m)
        {
            let name = ((new Date(y,m).toLocaleDateString('default', {month:'short'})).trim().split(" "))[1]
            return name
        },
        fnNOD(y,m)
        {
            let nod = new Date(y,m + 1,0).getDate()
            return nod
        },
        Next()
        {
            if (this.Months.Number == 11)
            {
                this.Months.Number = 0
                this.Months.Year++
                this.Months.Name = this.fnmonthday(this.Months.Year,this.Months.Number)
                this.Months.NOD = this.fnNOD(this.Months.Year,this.Months.Number)
            }
            else
            {
                this.Months.Number++
                this.Months.Name = this.fnmonthday(this.Months.Year,this.Months.Number)
                this.Months.NOD = this.fnNOD(this.Months.Year,this.Months.Number)
            }
            this.calculatemd()
 //можно увидеть что данные в объекте меняются
        },
        Back()
        {
            if (this.Months.Number == 0)
            {
                this.Months.Number = 11
                this.Months.Year--
                this.Months.Name = this.fnmonthday(this.Months.Year,this.Months.Number)
                this.Months.NOD = this.fnNOD(this.Months.Year,this.Months.Number)
            }
            else
            {
                this.Months.Number--
                this.Months.Name = this.fnmonthday(this.Months.Year,this.Months.Number)
                this.Months.NOD = this.fnNOD(this.Months.Year,this.Months.Number)
            }

            this.calculatemd()
        },
        nowMonth() {
            this.Months.Number = new Date().getMonth()
            this.Months.Year = new Date().getFullYear()
            this.Months.Name = this.fnmonthday(this.Year,this.Month)
            this.calculatemd()
        }
    },
    created() //задаются значения сегодняшней даты
    {
        this.initCal()
        this.calculatemd()
    }
};
</script>

<style>

.body {
   width: 1500px;
   height: 1300px;
   margin-top: 70px;
   margin-left: 250px;
}

.day {
    color: black;
    background-color: #F0F0F0;
    border-radius: 100%;
    padding: 35px;
    margin: 15px;
    margin-bottom: 20px;
    text-align: center;
}

.week {
    font-size: 17px;

}

.now-day {
    background-color: #0064ff;
    color: white
}

.btns {
    justify-content: space-between;
    padding: 100px; 
}

.btn {
    border-radius: 100px;
    background-color: #0064ff;
    color: white
}

.w
{
    background-color: green;
}
.q
{
    background-color: purple;
}
.e
{
background-color: brown;
}
.flex
{
    width: 500px;
    height: 60px;
    background-color: black;
}
.stack
{
    margin: 30px;
    padding-top: 17px;
    text-align: center;
    font-size: 20px;
    width: 700px;
    height: 150px;
    background-color: #0064ff;
    color: white;
    border-radius: 100%;
}
    .label1
    {
        background-color: red;
    }
    .label2
    {
        background-color: green;
    }



</style>
