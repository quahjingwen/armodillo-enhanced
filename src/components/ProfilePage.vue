/* eslint-disable */
<template>
  <div id="show-modules">
    <h1>Profile Page</h1>
    <div class='some-page-wrapper'>
      <div class='row'>
        <div class='column'>
          <div class='blue-column'>
            <center><h2>Student Details</h2>
            <img src="~../assets/image.jpg" width="200" height="220"></center>
            <p> {{ student.Name}} </p>
            <p> {{ student.Year}} </p>
            <p> {{ student.Grad}} </p>
            <p> {{ student.Program}} </p>
          </div>
        </div>
        <div class='column'>
          <div class='green-column'>
            <h2>Graduation Requirements</h2>
            <br>
            <u><h3>Graduation Progression</h3></u>
            <b-progress :value="progression" class="mb-3"></b-progress>
            <div class="progress-meter">
              <div class="meter meter-left" style="width: 25%;"><span class="meter-text">0MCS</span></div>
              <div class="meter meter-left" style="width: 25%;"><span class="meter-text">40MCS</span></div>
              <div class="meter meter-right" style="width: 25%;"><span class="meter-text">160MCS</span></div>
              <div class="meter meter-right" style="width: 25%;"><span class="meter-text">120MCS</span></div>
            </div>
            <br><br>
            <p><b> &#x25a2; No. of MCs completed: </b>{{totalMC}}/160MCs </p>
            <p><b>&#x25a2; ULR (GEM): </b> {{ sumGEM }}/{{Object.keys(this.student.GradReq.GEM).length.toString()}} Modules &#8594; {{ sumGEM*4 }}MCs/{{Object.keys(this.student.GradReq.GEM).length*4}}MCs</p>
            <p><b> &#x25a2; 1k Modules taken: </b>{{ sumLevel1 }}/{{Object.keys(this.student.GradReq.Level1).length.toString()}} Modules &#8594; {{ sumLevel1*4 }}MCs/{{Object.keys(this.student.GradReq.Level1).length*4}}MCs</p>
            <p><b>&#x25a2; Core Modules taken: </b>{{ sumCore }}/{{Object.keys(this.student.GradReq.Core).length.toString()}} Modules &#8594; {{ sumCore*4 }}MCs/{{Object.keys(this.student.GradReq.Core).length*4}}MCs</p>
            <p><b>&#x25a2; UEs taken: </b>{{ sumUE }}/{{Object.keys(this.student.GradReq.UEM).length.toString()}} Modules &#8594; {{ sumUE*4 }}MCs/{{Object.keys(this.student.GradReq.UEM).length*4}}MCs</p>
            <p><b> &#x25a2; Electives Taken: </b>{{totalElectives}} &#8594; {{ ElectivesMC}}MCs/24MCs</p>
            <ul id="example-1" style="padding-left:50px">
              <li>BT4101: {{bt4101Done}} </li>
              <li>List A: {{listA}} Modules</li>
              <li>List B: {{listB}} Modules</li>
              <li>List C: {{listC}} Modules</li>
            </ul>
            <p><b>&#x25a2; Industrial Attachment: </b> {{this.student.GradReq.Attachment.Done}}MCS/12MCS </p>
            <ul id="example-1" style="padding-left:50px">
              <li>{{iaDone}}</li>
              </ul>
              <p>Attachment Programmes Available (click for more details):</p>
              <ul id="example-1" style="padding-left:50px">
              <li><a href="https://www.comp.nus.edu.sg/studentlife/intern/atap/student/">Advanced Technology Attachment Programme (ATAP)</a></li>
              <li><a href="https://www.comp.nus.edu.sg/studentlife/intern/iip/student/">Industry Attachment Programme (IIP)</a></li>
            </ul>
            <h3><u>Degree Requirements</u></h3>
            <div class="card">
              <div class="card-header"><h3>Summary of degree requirements for BSc (Business Analytics)</h3></div>
              <div class="card-body">
                <p><b>Grand Total: 160 MCS</b></p>
                <p>*Highlight rows in green represent completion of module</p>
                <p> <u>1. University Level Requirements: Subtotal 20 MCS </u></p>
                <table class="table table-striped">
                  <thead>
                    <tr>
                      <th>Module Code</th>
                      <th>Completed</th>
                      <th>Modular Credits</th>
                      <th>Prerequisites</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(value,key) in student.GradReq.GEM" :key="value.id" :class="{'text-complete': completed(value) === 'Completed' }">
                      <td>{{ key }}</td>
                      <td >{{completed(value)}}</td>
                      <td>{{moreMC(key)}}</td>
                      <td>None</td>
                    </tr>
                  </tbody>
                </table>
                <p> <u>2. Programme Requirements: Subtotal 108 MCS </u></p>
                <p>2a. Core Modules: Subtotal 72 MCS</p>
                <table class="table table-striped">
                  <thead>
                    <tr>
                      <th>Module Code</th>
                      <th>Completed</th>
                      <th>Modular Credits</th>
                      <th>Prerequisites</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(value,key) in student.GradReq.Core" :key="value.id" :class="{'text-complete': completed(value) === 'Completed'}">
                      <td>{{ key }}</td>
                      <td>{{completed(value)}}</td>
                      <td>{{moreMC(key)}}</td>
                      <td>{{ Prereq['Core'][key] }}</td>
                    </tr>
                  </tbody>
                </table>
                <p>2b. Programme Electives: Subtotal 24 MCS</p>
                <p><b>Option 1:</b></p>
                <p>Choose 6 modules to make up 24 MCs from Lists A, B and C, with at least 2 modules each from List A and List B. 5 of 6 modules must be at level-4000. </p>
                <p><b>Option 2:</b></p>
                <p>Choose BT4101 (B.Sc. Dissertation) and 3 modules to make up 24 MCs from Lists A, B and C, with at least 1 module each from List A and List B. 2 of 3 modules must be at level-4000.</p>
                
                <p>BT4101</p>
                <table class="table table-striped">
                  <thead>
                    <tr>
                      <th>Module Code</th>
                      <th>Completed</th>
                      <th>Modular Credits</th>
                      <th>Prerequisites</th>
                    </tr>
                  </thead>
                  <tbody>
                      <td>BT4101</td>
                      <td :class="{'text-complete': completed(this.student.GradReq.ElecOpt.BT4101) === 'Completed'}">{{completed(this.student.GradReq.ElecOpt.BT4101)}}</td>
                      <td>12</td>
                      <td>{{ Prereq['BT4101'] }}</td>
                  </tbody>
                </table>
                
                <p>List A</p>
                <table class="table table-striped">
                  <thead>
                    <tr>
                      <th>Module Code</th>
                      <th>Completed</th>
                      <th>Modular Credits</th>
                      <th>Prerequisites</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(value,key) in student.GradReq.ElecOpt.A" :key="value.id" :class="{'text-complete': completed(value) === 'Completed'}">
                      <td>{{ key }}</td>
                      <td>{{completed(value)}}</td>
                      <td>{{moreMC(key)}}</td>
                      <td>{{ Prereq['A'][key] }}</td>
                    </tr>
                  </tbody>
                </table>

                <p>List B</p>
                <table class="table table-striped">
                  <thead>
                    <tr>
                      <th>Module Code</th>
                      <th>Completed</th>
                      <th>Modular Credits</th>
                      <th>Prerequisites</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(value,key) in student.GradReq.ElecOpt.B" :key="value.id" :class="{'text-complete': completed(value) === 'Completed'}">
                      <td>{{ key }}</td>
                      <td>{{completed(value)}}</td>
                      <td>{{moreMC(key)}}</td>
                      <td>{{ Prereq['B'][key] }}</td>
                    </tr>
                  </tbody>
                </table>

                <p>List C</p>
                <table class="table table-striped">
                  <thead>
                    <tr>
                      <th>Module Code</th>
                      <th>Completed</th>
                      <th>Modular Credits</th>
                      <th>Prerequisites</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(value,key) in student.GradReq.ElecOpt.C" :key="value.id" :class="{'text-complete': completed(value) === 'Completed'}">
                      <td>{{ key }}</td>
                      <td>{{completed(value)}}</td>
                      <td>{{moreMC(key)}}</td>
                      <td>{{ Prereq['C'][key] }}</td>
                    </tr>
                  </tbody>
                </table>

                <p>2c. IS4010 Industry Internship Programme </p>
                <table class="table table-striped">
                  <thead>
                    <tr>
                      <th>Module Code</th>
                      <th>Completed</th>
                      <th>Modular Credits</th>
                      <th>Prerequisites</th>
                    </tr>
                  </thead>
                  <tbody>
                      <td>IS4010</td>
                      <td :class="{'text-complete': completed(this.student.GradReq.Attachment) === 'Completed'}">{{completed(this.student.GradReq.Attachment)}}</td>
                      <td>12</td>
                      <td>[IS2101 or CS2101] and [IS1105 or IS3101 or IS3103] and [IS2103 or CS2107 or (BT2101 and BT2102)]</td>
                  </tbody>
                </table>
                <p> <u>3. Unrestricted Electives: Subtotal 32 MCS </u></p>
                <table class="table table-striped">
                  <thead>
                    <tr>
                      <th>Module Code</th>
                      <th>Completed</th>
                      <th>Modular Credits</th>
                    </tr>
                  </thead>
                  <tbody>
                      <td>UE</td>
                      <td :class="{'text-complete': completed(sumUE) === 'Completed'}">{{completed(sumUE)}}</td>
                      <td>{{ sumUE*4 }}MCs/{{Object.keys(this.student.GradReq.UEM).length*4}}MCs</td>
                  </tbody>
                </table>

              </div>
            </div>

          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
//import HelloWorld from './HelloWorld'
// import {db} from "@/firebase.js"
//import {seRef} from '@/firebase.js'

export default {
  name: 'Profile',
  components: {
    
  },
  data () {
    return {
      student: {
        Name: "Student Name",
        Year: "Year 18/19 Semester 2",
        Grad: "Expected Year of Graduation: 2022",
        Program: "SEP Y2S2 Approved",
        GradReq: {
          GEM: {GEH:0,GEQ:1,GER:1,GES:0, GET:0},
          "Core": {"BT1101":1,"CS1010S":1,"CS1020":1,"CS2010":0,"EC1301":1,"IS1103/X":0,"MA1101R":1,"MA1521":1,"MKT1705X":1,"BT2101":1,"BT2102":0,"IS2101":0,"ST2334":0,"BT3102":0,"BT3103":0,"IS3103":0,"BT4103":0},
          "ElecOpt":{
            "BT4101":0,
            "A": {"DBA3712":0,"IE3120":0,"IS3240":0,"BT4013":0,"BT4016":0,"BT4211":0,"BT4212":0,"DBA4811":0,"IS4241":0,"IS4250":0,"MKT4812":0},
            "B":{"IE2110":0,"CS3244":0,"DBA3803":0,"BSE4711":0,"BT4012":0,"BT4015":0,"BT4221":0,"BT4222":0,"BT4240":0,"IS4241":0,"IE4210":0,"ST3131":0,"ST4245":0},
            "C":{"IS3221":0,"IS3261":0,"BT4014":0,"IS4228":0,"IS4302":0}
          },
          "Attachment":{"Done":0},
          "UEM":{"UEM1":0,"UEM2":0,"UEM3":0,"UEM4":0,"UEM5":0,"UEM6":0,"UEM7":0,"UEM8":0},
          "Level1":{"GEH":0,"GEQ":1,"GER":1,"GES":0,"GET":0,"BT1101":1,"CS1010S":1,"CS1020":1,"EC1301":1,"IS1103/X":0,"MA1101R":1,"MA1521":1,"MKT1705X":1,"mod1":0,"mod2":0}
        }
      },
      Prereq: {
        Core: {
          "BT1101":"None",
          "CS1010S":"None",
          "CS1020":"CS1010",
          "CS2010":"CS1020 or CS1020E or CG1103",
          "EC1301":"None",
          "IS1103/X":"None",
          "MA1101R":"None",
          "MA1521":"None",
          "MKT1705X":"None",
          "BT2101":"(CS1010 or its equivalent) and (MA1521 or MA1102R) and BT1101",
          "BT2102":"(CS1010 or its equivalent) and BT1101",
          "IS2101":"ES1000 and/or ES1102/ES1103 for students who are required to take",
          "ST2334":"MA1102R or MA1312 or MA1505 or MA1507 or MA1521",
          "BT3102":"BT2101 and (CS1020/E or CS2020 or CS2030 or CS2103/T or CS2113/T)",
          "BT3103":"BT2102 ",
          "IS3103":"(IS1103 or equivalent) and (CS2101 or IS2101)",
          "BT4103":"BT2101 and BT2102 and IS2101"
          },
          BT4101: 'Attained at least 70% of the MC requirement for degree',
          A: {
            "DBA3712":'DAO2702',
            "IE3120":'IE2100 or DBA3711',
            "IS3240":'IS1103/X and (IS2102 or BT2102)',
            "BT4013":'BT3102',
            "BT4016":'BT2101 and BT2102',
            "BT4211":'MKT1705X and [(BT2101 and BT2102) or (DBA3803 and IT3010)]',
            "BT4212":'CS1010S or its equivalent and BT2101 and ST2334',
            "DBA4811":'DAO2702',
            "IS4241":'[(CS1010 or equivalent) and (IS1103 or IS1103FC or IS1103X)] or [(CS1010 or equivalent) and BT1101] or [DAO2702 and IT3010]',
            "IS4250":'IS1103 or equivalent',
            "MKT4812":'MKT1705/MKT1705X or RE3704.'
          },
          B: {
            "IE2110":'None',
            "CS3244":'(CS2010 or CS2020 or CS2040 or CS2040C) and (ESP1107 or ESP2107 ST1232 or ST2131 or ST2132 or ST2334) and (MA1102R or MA1505 or (MA1511 and MA1512) or MA1521) and (MA1101R or MA1311 or MA1506 or MA1508E)',
            "DBA3803":'DAO2702',
            "BSE4711":'None',
            "BT4012":'BT3102',
            "BT4015":'None',
            "BT4221":'BT2101 and BT2102 and (CS2010 or CS2020 or CS2040/C)',
            "BT4222":'[(CS1010 or equivalent) and BT2101 and BT2102] or [DAO2702 and DBA3803 and IT3010]',
            "BT4240":'[MA1311 or MA1101R] and [MA1521 or MA1102R] and BT2101',
            "IS4241":'[(CS1010 or equivalent) and (IS1103 or IS1103FC or IS1103X)] or [(CS1010 or equivalent) and BT1101] or [DAO2702 and IT3010]',
            "IE4210":'IE2110',
            "ST3131":'ST2131 or MA2216 or ST2334',
            "ST4245":'ST3131'
          },
          C: {
            "IS3221":'[(CS1010 or equivalent) and (IS1103 or IS1103FC or IS1103X)] or [(CS1010 or equivalent) and BT1101] or [DAO2702 and IT3010]',
            "IS3261":'(CS1020 or equivalent) or CS2020 or CS2030 or CS2040/C',
            "BT4014":'BT2102',
            "IS4228":'IS3101 or IS3103',
            "IS4302":'(CS2102 or BT2102) and (CS1020 or its equivalent or CS2030 or CS2103/T or CS2113/T)'
          }
        }
      }
    },
  methods: {
    completed: function(value) {
      if (value ==1) {
        return "Completed";
      }
      else if (value ==32) {
        return "Completed";
      }
      else {
        return "Incomplete"
      }
    },
    moreMC: function(key) {
      if (key=="BT4103") {
        return 8
      }
      else {
        return 4
      }
    }
  },
  computed: {
    sumGEM: function () {
      let sum = 0;
      for (let i =0; i< Object.keys(this.student.GradReq.GEM).length; i++) {
        sum += Object.values(this.student.GradReq.GEM)[i]
      }
      return sum
    },
    sumLevel1: function () {
      let sum = 0;
      for (let i =0; i< Object.keys(this.student.GradReq.Level1).length; i++) {
        //console.log(Object.values(this.student.GradReq.Level1)[i])
        sum += Object.values(this.student.GradReq.Level1)[i]
      }
      return sum
    },
    sumCore: function () {
      let sum = 0;
      for (let i =0; i< Object.keys(this.student.GradReq.Core).length; i++) {
        //console.log(Object.values(this.student.GradReq.Core)[i])
        sum += Object.values(this.student.GradReq.Core)[i]
      }
      return sum 
    },
    sumUE: function () {
      let sum = 0;
      for (let i =0; i< Object.keys(this.student.GradReq.UEM).length; i++) {
        //console.log(Object.values(this.student.GradReq.UEM)[i])
        sum += Object.values(this.student.GradReq.UEM)[i]
      }
      return sum
    },
    iaDone: function () {
      if (this.student.GradReq.Attachment === 1) {
        return "Done"
      }
      return "Not Done"
    },
    bt4101Done: function () {
      if (this.student.GradReq.ElecOpt.BT4101 === 1) {
        return "Done"
      }
      return "Not Done"
    },
    ElectivesMC: function () {
      let sum = 0;
      if (this.student.GradReq.ElecOpt.BT4101===1) {
        sum += 12
      }
      //console.log(Object.keys(this.student.GradReq.ElecOpt).length-1)
      for (let i =0; i< Object.keys(this.student.GradReq.ElecOpt.A).length; i++) {
        if (Object.values(this.student.GradReq.ElecOpt.A)[i] ===1) {
            sum +=4;
        }
      }
      for (let i =0; i< Object.keys(this.student.GradReq.ElecOpt.B).length; i++) {
        if (Object.values(this.student.GradReq.ElecOpt.B)[i] ===1) {
            sum +=4;
        }
      }
      for (let i =0; i< Object.keys(this.student.GradReq.ElecOpt.C).length; i++) {
        if (Object.values(this.student.GradReq.ElecOpt.C)[i] ===1) {
            sum +=4;
        }
      }
      return sum
    },
    totalElectives: function() {
      let sum = 0;
      if (this.student.GradReq.ElecOpt.BT4101===1) {
        sum += 1
      }
      //console.log(Object.keys(this.student.GradReq.ElecOpt).length-1)
      for (let i =0; i< Object.keys(this.student.GradReq.ElecOpt.A).length; i++) {
        if (Object.values(this.student.GradReq.ElecOpt.A)[i] ===1) {
            sum +=1;
        }
      }
      for (let i =0; i< Object.keys(this.student.GradReq.ElecOpt.B).length; i++) {
        if (Object.values(this.student.GradReq.ElecOpt.B)[i] ===1) {
            sum +=1;
        }
      }
      for (let i =0; i< Object.keys(this.student.GradReq.ElecOpt.C).length; i++) {
        if (Object.values(this.student.GradReq.ElecOpt.C)[i] ===1) {
            sum +=1;
        }
      }
      return sum
    },
    listA: function () {
      let sum=0;
      for (let i =0; i< Object.keys(this.student.GradReq.ElecOpt.A).length; i++) {
        if (Object.values(this.student.GradReq.ElecOpt.A)[i] ===1) {
            sum +=1;
        }
      }
      return sum
    },
    listB: function () {
      let sum=0;
      for (let i =0; i< Object.keys(this.student.GradReq.ElecOpt.B).length; i++) {
        if (Object.values(this.student.GradReq.ElecOpt.B)[i] ===1) {
            sum +=1;
        }
      }
      return sum
    },
    listC: function () {
      let sum=0;
      for (let i =0; i< Object.keys(this.student.GradReq.ElecOpt.C).length; i++) {
        if (Object.values(this.student.GradReq.ElecOpt.C)[i] ===1) {
            sum +=1;
        }
      }
      return sum;
    },
    // to be updated
    totalMC: function () {
      let countable = this.sumUE + this.sumCore + this.sumGEM + this.student.GradReq.Level1.mod1+ this.student.GradReq.Level1.mod2;
      countable = countable*4
      if (this.student.GradReq.Attachment ===1) {
        countable += 12
      }
      if (this.student.GradReq.ElecOpt.BT4101===1) {
        countable += 12
      }
      //console.log(Object.keys(this.student.GradReq.ElecOpt).length-1)
      for (let i =0; i< Object.keys(this.student.GradReq.ElecOpt.A).length; i++) {
        if (Object.values(this.student.GradReq.ElecOpt.A)[i] ===1) {
            countable +=4;
        }
      }
      for (let i =0; i< Object.keys(this.student.GradReq.ElecOpt.B).length; i++) {
        if (Object.values(this.student.GradReq.ElecOpt.B)[i] ===1) {
            countable +=4;
        }
      }
      for (let i =0; i< Object.keys(this.student.GradReq.ElecOpt.C).length; i++) {
        if (Object.values(this.student.GradReq.ElecOpt.C)[i] ===1) {
            countable +=4;
        }
      }
      return countable
    },
    progression: function(){
      return this.totalMC/160*100
    },
  }
}
</script>

<style>

#show-modules {
  max-width: 1200px;
  margin:0 auto;
}

#example-1 {
  text-indent: 20px;
}

.some-page-wrapper {
  margin: 0px;
  background-color: #ffffff;
}

.row {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  width: 100%;
}

.column {
  display: flex;
  flex-direction: column;
  flex-basis: 100%;
  flex: 1;
  text-align: left;
}

.blue-column {
  background-color: #F8F8F8;
  height: 450px;
  margin: 20px;
  width: 300px;
  padding-top: 20px;
  padding-left: 20px;
  padding-right: 20px;
}

.green-column {
    background-color: #F8F8F8;
    margin: 20px;
    width: 800px;
    padding-top: 20px;
    padding-left: 30px;
    padding-right: 30px;
}

table {
  border-collapse: separate;
  border-spacing: 0;
  color: #4a4a4d;
  font: 14px/1.4 "Helvetica Neue", Helvetica, Arial, sans-serif;
}
th,
td {
  padding: 10px 15px;
  vertical-align: middle;
}
thead {
  background: #395870;
  background: linear-gradient(#49708f, #293f50);
  color: #fff;
  font-size: 11px;
  text-transform: uppercase;
}
th:first-child {
  border-top-left-radius: 5px;
  text-align: left;
}
th:last-child {
  border-top-right-radius: 5px;
}
tbody tr:nth-child(even) {
  background: #f0f0f2;
}
td {
  border-bottom: 1px solid #cecfd5;
  border-right: 1px solid #cecfd5;
}
td:first-child {
  border-left: 1px solid #cecfd5;
}
.book-title {
  color: #395870;
  display: block;
}
.text-offset {
  color: #7c7c80;
  font-size: 12px;
}
.item-stock,
.item-qty {
  text-align: center;
}
.item-price {
  text-align: right;
}
.item-multiple {
  display: block;
}
tfoot {
  text-align: right;
}
tfoot tr:last-child {
  background: #f0f0f2;
  color: #395870;
  font-weight: bold;
}
tfoot tr:last-child td:first-child {
  border-bottom-left-radius: 5px;
}
tfoot tr:last-child td:last-child {
  border-bottom-right-radius: 5px;
} 

.text-complete {
    background-color: #66ff00 !important;
  }

.box1{
  width: 300px;
  height: 80px;
  display: inline-block; /* Change this to block and see what happens */
  position:relative;
  }

.progress-meter {
	min-height: 15px;
	border-bottom: 2px solid rgb(160, 160, 160);
}

.progress-meter > .meter {
	position: relative;
	float: left;
	min-height: 15px;
	border-width: 0px;
	border-style: solid;
	border-color: rgb(160, 160, 160);
}

.progress-meter > .meter-left {
	border-left-width: 2px;
}

.progress-meter > .meter-right {
	float: right;
	border-right-width: 2px;
}

.progress-meter > .meter-right:last-child {
	border-left-width: 2px;
}

.progress-meter > .meter > .meter-text {
	position: absolute;
	display: inline-block;
	bottom: -20px;
	width: 100%;
	font-weight: 700;
	font-size: 0.85em;
	color: rgb(160, 160, 160);
	text-align: left;
}

.progress-meter > .meter.meter-right > .meter-text {
	text-align: right;
}
</style>
