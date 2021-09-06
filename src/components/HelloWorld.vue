<template>
  <v-container fluid>
    <v-card>

      <!-- first row heading & buttons -->

      <v-row class="ma-1">
        <v-col cols="auto">
          <h4 class="text-left pt-2">
            <v-avatar color="white" size="25" class="elevation-1 mr-1">
              <v-icon color="primary" size="15">mdi-clipboard-file</v-icon>
            </v-avatar>
            <span >My Tasks</span>
          </h4>
        </v-col>
        <v-spacer></v-spacer>
        <v-col cols="5" class="d-flex justify-center">
          <v-text-field prepend-inner-icon="mdi-magnify" class="mr-2" outlined label="Search" dense hide-details></v-text-field>
          <v-btn dense outlined class="mr-2"><v-icon size="20">mdi-filter-outline</v-icon>Filter</v-btn>
          <v-btn dense outlined max-width="60px"><v-icon size="20">mdi-filter-outline</v-icon></v-btn>
        </v-col>
      </v-row>

      <!-- second row task cards -->
      
      <v-row class="second-row d-flex justify-center grey lighten-3" no-gutters>
        <v-col cols="10" class="d-flex justify-center px-8" style="margin-top:60px;font-size:14px;">
          <v-col cols="auto">Name</v-col><v-spacer></v-spacer>
          <v-col cols="auto">Assigned Date</v-col><v-spacer></v-spacer>
          <v-col cols="auto">Reccuring</v-col><v-spacer></v-spacer>
          <v-col cols="auto">Action Required</v-col><v-spacer></v-spacer>
          <v-col cols="auto">Beneficiary</v-col><v-spacer></v-spacer>
          <v-col cols="auto">More</v-col>
        </v-col>
        <v-col cols="10" class="pt-0">
          <div style="height:450px" class="v-scrolling-div">
            <v-expansion-panels style="box-shadow: none">
              <v-expansion-panel v-for="item in taskCardDetails" :key="item.id" class="mb-3 pt-0">
                <v-expansion-panel-header hide-actions expand-icon="mdi-border-outside" style="height:100px;" >
                  <v-row class="" no-gutters>
                    <v-col cols=11 class="pt-2">
                      <h4 style="font-size:16px;font-weight:bold" class="pt-2">{{item.taskName}}</h4>
                      <v-row>
                        <v-col cols="12" class="d-flex justify-center">
                          <v-col cols="auto" class="mx-0 px-0">
                            <v-avatar size="20" style="background-color:black"><span style="color:white;font-size:10px">{{item.responses}}</span></v-avatar>
                            <v-chip small style="width:100px;" class="mx-4 px-3" :class="{'task-current-chip' :item.taskStatus=='Current','task-approve-chip' :item.taskStatus=='Approved','task-complete-chip' :item.taskStatus=='Completed'}" label>{{item.taskStatus}}</v-chip>
                          </v-col>
                          <v-spacer></v-spacer>
                          <v-col cols="auto">
                            <v-avatar size="25" class="elevation-1 blue lighten-5"><v-icon size="15" color="primary">mdi-calendar</v-icon></v-avatar>
                            <span class="mx-4">{{item.AssignedDate}}</span>
                          </v-col>
                          <v-spacer></v-spacer>
                          <v-col cols="auto">
                            <v-avatar size="25" class="elevation-1 blue lighten-5"><v-icon size="15" color="primary">mdi-calendar-month</v-icon></v-avatar>
                            <span class="mx-4">{{item.DurationType}}</span>
                          </v-col>
                          <v-spacer></v-spacer>
                          <v-col cols="auto">
                            <v-avatar size="25" class="elevation-1 blue lighten-5"><v-icon size="15" color="primary">mdi-pulse</v-icon></v-avatar>
                            <span class="mx-4">{{item.dataType}}</span>
                          </v-col>
                          <v-spacer></v-spacer>
                          <v-col cols="auto">
                            <v-avatar size="25" class="elevation-1 blue lighten-5"><v-icon size="15" color="primary">mdi-account-outline</v-icon></v-avatar>
                            <span class="mx-4">{{item.beneficiary}}</span>
                          </v-col>
                          <v-spacer></v-spacer>
                          <v-col cols="auto">
                            <v-icon small style="position:relative;left:20px" >mdi-dots-vertical</v-icon>
                          </v-col>
                        </v-col>
                      </v-row>
                    </v-col>
                    <v-spacer></v-spacer>
                    <v-col cols="1">
                      <div id="growContainer" class="text-center">
                          <div class="grow" :class="{'task-activity-chip' :item.taskType=='Outputs','task-outcome-chip' :item.taskType=='Outcomes','task-risk-chip' :item.taskType=='Risk','task-survey-chip' :item.taskType=='Survey'}">
                            <span class="hide">{{item.taskType}}</span>
                          </div>
                      </div>
                    </v-col>
                  </v-row>
                </v-expansion-panel-header>
                <v-divider></v-divider>
                <v-expansion-panel-content @click.native="openDialog=true">
                  <div class="container ma-0 pa-0">
                    <div class="inner-container ma-0 pa-0" v-for="(user,index) in userDetais" :key="index">
                      <div class="inner-inner-container" style="width:100%">
                        <span></span>
                        <span class="username">
                          {{user.Name}}
                        </span>
                        <span class="AssignedDate">
                          {{user.AssignedDate}}
                        </span>
                        <span class="userType">
                          {{user.Type}}
                        </span>
                        <span class="usercomment">
                          {{user.comment}}
                        </span>
                      </div>
                    </div>
                    <!-- <v-row>
                      <v-col cols="12" v-for="(user,index) in userDetais" :key="index" class="d-flex justify-center dropdown_container pt-8">
                        <v-col cols="2" class="ma-0 pa-0">
                          <p>{{user.Name}}</p>
                        </v-col>
                        <v-spacer></v-spacer>
                        <v-col cols="3" class="ma-0 pa-0">
                          <p style="position:relative;left:30px">{{user.AssignedDate}}</p>
                        </v-col>
                        <v-spacer></v-spacer>
                        <v-col cols="4" class="ma-0 pa-0">
                          <p>{{user.Type}}</p>
                        </v-col>
                        <v-spacer></v-spacer>
                        <v-col cols="3" class="ma-0 pa-0">
                          <p>{{user.comment}}</p>
                        </v-col>
                      </v-col>
                    </v-row> -->
                  </div>
                </v-expansion-panel-content>
              </v-expansion-panel>
            </v-expansion-panels>
          </div>
        </v-col>
      </v-row>
      <template>
        <v-dialog v-model="openDialog" persistent>
        <v-card class="right-fixed-panel">
          <v-row>
            <v-col cols="auto">
              <h4>Baseline Survey</h4>
            </v-col>
            <v-spacer></v-spacer>
            <v-col cols="auto">
              <v-icon @click="openDialog=flase" size="30" color="black">mdi-close</v-icon>
            </v-col>
          </v-row>
          <v-row class="d-flex justify-center grey lighten-3" no-gutters>
            <v-col cols="12">
              <h3>Lorem ipsum dolor sit amet consectetur adipisicing elit. Aspernatur eligendi officia, tempora blanditiis exercitationem eius laborum dignissimos harum? Voluptas eaque ullam provident perferendis hic exercitationem accusamus aut vero quam veritatis?
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusantium sint, facere, veniam debitis dolorum incidunt laboriosam consequatur aliquam, ipsam maxime magni totam ut! Quidem fugiat ab delectus cum tenetur sed!Lorem
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Numquam obcaecati aut accusamus assumenda. Minus laudantium repellat, eveniet porro eos velit sed doloremque suscipit pariatur quisquam rem recusandae laboriosam labore quasi!
              </h3>
            </v-col>
          </v-row>
          <v-btn @click="openDialog=flase" type="submit" class="primary pa-2">close</v-btn>
        </v-card>
      </v-dialog>
      </template>

    </v-card>
  </v-container>
</template>

<script>
export default {
  name: "HelloWorld",

  data: () => ({
    openDialog: false,
    taskCardDetails:[
      {taskName:"Baseline Survey",responses:12,taskStatus:"Current",AssignedDate:"12/09/2021",DurationType:"Monthly",dataType:"Data Collect",beneficiary:"Teachers",id:1,taskType:"Survey"},
      {taskName:"Percentage of decrease in plantation cost",responses:4,taskStatus:"Approved",AssignedDate:"12/09/2021",DurationType:"Monthly",dataType:"Data Collect",beneficiary:"Teachers",id:2,taskType:"Outputs"},
      {taskName:"Percentage of decrease in natural cost",responses:10,taskStatus:"Completed",AssignedDate:"12/09/2021",DurationType:"Monthly",dataType:"Data Collect",beneficiary:"Teachers",id:3,taskType:"Outcomes"},
      {taskName:"Natural disaster",responses:8,taskStatus:"Current",AssignedDate:"12/09/2021",DurationType:"Monthly",dataType:"Data Collect",beneficiary:"Teachers",id:4,taskType:"Risk"},
    ],
    userDetais:[
      {Name:"koushik",AssignedDate:"Aug 15 8:30 AM",Type:"Reimbursement requested",comment:"goodgoodgoodgoodgood"},
      {Name:"Kishore",AssignedDate:"Aug 15 8:30 AM",Type:"Reimbursement requested",comment:"good"},
      {Name:"Sanjay",AssignedDate:"Aug 15 8:30 AM",Type:"Reimbursement requested",comment:"good"},
      {Name:"Melvin",AssignedDate:"Aug 15 8:30 AM",Type:"Reimbursement requested",comment:"good"},
      {Name:"Regeesh",AssignedDate:"Aug 15 8:30 AM",Type:"Reimbursement requested",comment:"good"},
      {Name:"Subhash",AssignedDate:"Aug 15 8:30 AM",Type:"Reimbursement requested",comment:"good"},
      {Name:"Tony",AssignedDate:"Aug 15 8:30 AM",Type:"Reimbursement requested",comment:"good"},
    ]
  }),
};
</script>

<style scoped>

.right-fixed-panel{
  position: absolute;
  top: 0px;
  right: 0px;
  width: 60%;
  height: 100vh;
  padding: 30px 20px 10px 20px;

}

.task-current-chip{
  background-color: orange;
  color: white;
  text-align: center;
}

.task-approve-chip{
  background-color: lightgreen;
  color: green;
  text-align: center;
}

.task-complete-chip{
  background-color: violet;
  color: white;
  text-align: center;
}

.task-survey-chip{
  background-color: lightskyblue;
  color: rgb(0, 0, 255);
}

.task-activity-chip{
  background-color: lightgreen;
  color: green;
}

.task-outcome-chip{
  background-color: rgba(45, 235, 188, 0.973);
  color: orange;
}

.task-risk-chip{
  background-color: lightpink;
  color: rgb(240, 38, 72);
}

.inner-container .AssignedDate{
  position: absolute;
  left: 200px;
}

.inner-container .userType{
  position: absolute;
  left: 400px;
}

.inner-container .usercomment{
  position: absolute;
  left: 700px;
}

.inner-inner-container{
  line-height: 3rem;
  position: relative;
  left: 20px;
}

.container .inner-container{
  position: relative;
}

.container .inner-container::before{
  content: '';
  position: absolute;
  top: 0px;
  left: -10px;
  width: 0px;
  height:100%;
  border: 5px solid lightgray;
}

.container .inner-container .inner-inner-container::before{
  content: '';
  position: absolute;
  top: 17px;
  left: -30px;
  width: 10px;
  height:10px;
  border: 1px solid black;
  border-radius: 50%;
  background-color: black;
  
} 


.second-row{
  height: 85vh;
}

.inner-class-1{
  margin-top: 70px;
}

#growContainer{
	display: table;
  height: 100px;
}
.grow{
	display: table-cell;
  margin: 0px;
  padding: 0px 2px 0px 6px;
	width: 10px;
  height: 100px;
  position: relative;
  left: 60px;
	-webkit-transition:width 300ms;
	-moz-transition:width 300ms;
	transition:width 300ms;
  transition-timing-function: linear;
  -ms-writing-mode: tb-lr;
  -webkit-writing-mode: vertical-lr;
  -moz-writing-mode: vertical-lr;
  -ms-writing-mode: vertical-lr;
  writing-mode: vertical-lr;
}

#growContainer:hover .grow:hover {
	width:30px;
}

.hide{
  display: none;
}

.grow:hover .hide {
  display: block;
}

.v-scrolling-div {
    overflow-y: scroll;

    }
.v-scrolling-div::-webkit-scrollbar {
        width: 5px;
    }

.v-scrolling-div::-webkit-scrollbar-track {
        background: #f1f1f1;
    }

.v-scrolling-div::-webkit-scrollbar-thumb {
        background: #AFAFAF;
    }

.v-expansion-panel-header{
  padding: 0px 0px 0px 30px;
}


</style>