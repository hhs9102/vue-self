<template>
    <div>
        <h1>{{title}}</h1>
        <br/>
        Welcome to home!
        <br/>
        <input type="text" v-model="inputValue" style="width: 300px"/>
        <button @click="showAlertInputValue" style="width: 100px; height: 30px">alert</button>
        <button @click="setData" style="width: 100px; height: 30px">setData</button>
        <br/>
        <select v-model="region" @change="changeRegion">
            <!-- 콜론을 쓰면 바로 데이터에 접근이 가능하다. -->
            <option :key="i" :value="d.v" v-for="(d,i) in options">{{d.t}}</option>
        </select>
        <br/>
        <br/>

        <label>
            <input id="toggleTableView"
                   name="toggleTableView"
                   type="checkbox"
                   checked="checked"
                   @click="toggleTableView()"
            />
            toggle table view
        </label>

        <table v-if="tableShow==true">
            <tr :key="i" v-for="(d,i) in options" class="table table-bordered">
                <td>{{d.v}}</td>
                <td>{{d.t}}</td>
            </tr>
        </table>
    </div>
</template>
<script>
    export default {
        name: "Home",
        data(){
            return{
                title: "Home title",
                inputValue: "This is input Value(2 way)",
                options: [
                    {v:"S", t:"Seoul"},
                    {v:"B", t:"Busan"},
                    {v:"J", t:"Jeju"}
                ],
                region: "J", //select combobox에 대한 default 값 할당
                tableShow: true
            };
        },
        watch:{
            inputValue(){
                console.log("changedValue: " + this.inputValue);
            },
            tableShow(){
                console.log("tableShow: "+this.tableShow);
            }
        },
        methods: {
            showAlertInputValue(){
                alert(this.inputValue);
            },

            setData(){
                this.inputValue = "setData";
            },

            changeRegion(){
                alert(this.region+"(으)로 변경되었습니다.");
            },

            toggleTableView(){
                this.tableShow = !this.tableShow;
            }
        },

        beforeCreate() {
            console.log("beforeCreate")
        },
        created() { //DB를 통해 가져오고 mounted되기전에 가공하면 됨
            console.log("created")
        },
        beforeMount() {
            console.log("beforeMount")
        },
        mounted() {
            console.log("mounted")
        },
        beforeUpdate() {    //데이터 변경 전
            console.log("beforeUpdate")
        },
        updated() {         //데이터 변경 후
            console.log("updated")
        },
        beforeDestroy() {
            console.log("beforeDestroy")
        },
        destroyed() {
            console.log("destroyed")
        }
    };
</script>