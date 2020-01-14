<template>
  <div>
    <!--
    <h3 class="displayInfo">Number of available nurses : {{nursesAvailable}} &nbsp;</h3>
    <h3 class="displayInfo">Number of available physician : {{physiciansAvailable}} &nbsp;-</h3>
    <h3 class="displayInfo">Number of available roomsAvailable : {{roomsAvailable}} &nbsp;-</h3>
    <h3 class="displayInfo">Number of patients arrived: {{patientsArrived}} &nbsp;-</h3>
    <h3 class="displayInfo">Number of patients with paperwork to fill: {{paperworkToFill}} &nbsp;-</h3>
    <h3 class="displayInfo">Number of patients with paperwork filled: {{paperworkFilled}} &nbsp;-</h3>
    <h3 class="displayInfo">Number of patients with paperwork process finished: {{paperworkProcessFinished}} &nbsp;-</h3>
    <h3 class="displayInfo">Number of patients waiting in emergency room: {{patientsWaitingInEmergencyRoom}} &nbsp;-</h3>
    <h3 class="displayInfo">Number of patients under treatment: {{patientsUnderTreatment}} &nbsp;-</h3>
    <h3 class="displayInfo">Number of patients healed: {{patientsHealed}} &nbsp;-</h3>
    <h3 class="displayInfo">Number of requests for a room: {{messagesAskingForRoom}} &nbsp;-</h3>
    <h3 class="displayInfo">Number of requests for a physician: {{messagesAskingForPhysicians}} &nbsp;-</h3>
    <h3 class="displayInfo">Total patients under treatment: {{totalPatientsBeforeTreatment}} &nbsp;-</h3>
    <br/>
    -->
    
    <table>
      <thead>
        <tr>
          <th>current resources</th>
        </tr>
        
      </thead>
      <tbody>
        <tr>
          <td>Number of available nurses:{{nursesAvailable}}</td>
        </tr>
        <tr>
          <td>Number of available physician:{{physiciansAvailable}}</td>
        </tr>
        <tr>
          <td>Number of available rooms:{{roomsAvailable}}</td>
        </tr>
      </tbody>
      
    </table>
    <br/>
    <table>
      <thead>
        <tr>
           <th>global stats</th> 
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Number of patient welcomed:{{totalPatientsWelcomed}}</td>
        </tr>
        <tr>
          <td>Total number of patient healed:{{totalPatientsHealed}}</td>
        </tr>
      </tbody>
    </table>
    <br/>
    
    
    <table>
      <thead>
        <tr>
          <td>patient comes in</td>
          <td>patient fills the paperwork</td>
          <td>paperwork filled</td>
          <td>paperwork processed by nurse finished</td>
          <td>patients waiting in emergency room</td>
          <td>patients under treatment</td>
          <td>patients is healed waiting for checkout</td>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>
            <li v-for="item in patientsArrived" :key="item.nameOfClient">
              {{ item.nameOfClient }}
            </li>
          </td>
          <td>
            <li v-for="item in paperworkToFill" :key="item.nameOfClient">
              {{ item.nameOfClient }}
            </li>
          </td>
          <td>
            <li v-for="item in paperworkFilled" :key="item.nameOfClient">
              {{ item.nameOfClient }}
            </li>
          </td>
          <td>
            <li v-for="item in paperworkProcessFinished" :key="item.nameOfClient">
              {{ item.nameOfClient }}
            </li>
          </td>
          <td>
            <li v-for="item in patientsWaitingInEmergencyRoom" :key="item.nameOfClient">
              {{ item.nameOfClient }}
            </li>
          </td>
          <td>
            <li v-for="item in patientsUnderTreatment" :key="item.nameOfClient">
              {{ item.nameOfClient }}
            </li>
          </td>
          <td>
            <li v-for="item in patientsHealed" :key="item.nameOfClient">
              {{ item.nameOfClient }}
            </li>
          </td>
        </tr>
      </tbody>
    </table>
    
    <br/>
    <br/>
    <br/>
    <table>
      <thead>
        <tr>
          <th>change time</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><button v-on:click="addASecond">Add a second</button></td>
        </tr>
      </tbody>
    </table>
    <br/>
    <table>
      <thead>
        <tr>
          <th colspan="2">Processes of taking care of the patient</th>
        </tr>
      </thead>
      <tbody> 
        <tr>
          <td><button v-on:click="patientComesIn">Patients comes in</button></td>
        </tr>
        <tr>
          patient id:<input v-model="clientToRefuse">
        </tr>
        <tr>
          <td><button v-on:click="acceptPatient(clientToRefuse)">Accept patient</button></td>
          <td><button v-on:click="patientRefused(clientToRefuse)">Refuse patient</button></td>
        </tr>
        <tr>
          <td><button v-on:click="fillsPaperwork(clientToRefuse)">Fills paperwork</button></td>
        </tr>
        <tr>
          <td><button v-on:click="processPaperwork(clientToRefuse)">Process paperwork</button></td>
        </tr>
        <tr>
          <td><button v-on:click="goesInEmergencyRoom(clientToRefuse)">Goes in emergency room</button></td>
        </tr>
        <tr>
          <td><button v-on:click="startTreatment(clientToRefuse)">Start treatment</button></td>
        </tr>
        <tr>
          <td><button v-on:click="treatmentFinished(clientToRefuse)">Treatment finished</button></td>
        </tr>
        <tr>
          <td><button v-on:click="patientChecksOut(clientToRefuse)">Patient checks out</button></td>
        </tr>
      </tbody>
    </table>
    <br/>
    <table>
      <thead>
      </thead>
      <tbody>
        <tr>
          <table>
            <thead>
              <tr>
                <th colspan="2">Request and offer rooms</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><button v-on:click="requestForARoom">Request for a room</button></td>
                <td><button v-on:click="offersARoom">Offers a room</button></td>
              </tr>
              <tr>
                <td><button v-on:click="outsideAsksForARoom">Outside asks for a room</button></td>
                <td><button v-on:click="outsideOffersARoom">Outside offers a room</button></td>
              </tr>
            </tbody>
          </table>
        </tr>
        <tr>
          
          <table>
            <thead>
              <tr>
                <th colspan="2">Request and offer physician</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><button v-on:click="requestFormAPhysician">Request for a physician</button></td>
                <td><button v-on:click="offersAPhysician">Offers a physician</button></td>
              </tr>
              <tr>
                <td><button v-on:click="outsideAsksForAPhysician">Outside asks for a physician</button></td>
                <td><button v-on:click="outsideOffersAPhysician">Outside offers a physician</button></td>
              </tr>
            </tbody>
          </table>
        </tr>
      </tbody>
    </table>
      

    
    
    
    
    
    <button v-on:click="patientComesIn">Patients comes in</button>
    <button v-on:click="patientRefused(clientToRefuse)">Patient refused</button>
    <button v-on:click="acceptPatient(clientToRefuse)">Accept patient</button>
    <button v-on:click="fillsPaperwork(clientToRefuse)">Fills paperwork</button>
    <button v-on:click="processPaperwork(clientToRefuse)">Process paperwork</button>
    <button v-on:click="goesInEmergencyRoom(clientToRefuse)">Goes in emergency room</button>
    <button v-on:click="startTreatment(clientToRefuse)">Start treatment</button>
    <button v-on:click="treatmentFinished(clientToRefuse)">Treatment finished</button>
    <button v-on:click="patientChecksOut(clientToRefuse)">Patient checks out</button>
    <button v-on:click="requestForARoom">Request for a room</button>
    <button v-on:click="offersARoom">Offers a room</button>
    <button v-on:click="outsideAsksForARoom">Outside asks for a room</button>
    <button v-on:click="outsideOffersARoom">Outside offers a room</button>
    <button v-on:click="rejectDemandForRoom">Reject demand for a room</button>
    
    
    
    
    <button v-on:click="rejectDemandForPhysician">Reject demand for a physician</button>
    <br/>
    <button v-on:click="addASecond">Add a second</button>
    <button v-on:click="launchAutonomousSystem">Launch system</button>
  </div>
</template>

<script>
export default {
  name: 'clinic',
  data: function () {
    return {
      patientsArrived: [],
      paperworkToFill: [],
      paperworkFilled: [],
      paperworkProcessFinished: [],
      patientsWaitingInEmergencyRoom: [],
      patientsUnderTreatment: [],
      patientsHealed: [],
      nursesAvailable: 5,
      roomsAvailable: 5,
      physiciansAvailable: 5,
      messagesAskingForRoom: [],
      messagesAskingForPhysicians: [],
      totalPatientsBeforeTreatment: 0,
      totalPatientsWelcomed: 0,
      totalPatientsHealed:0,
      clientToRefuse: -1,
      youRequestedARoom: false,
      youRequestedAPhysician: false
    }
  },
  methods: {
    patientComesIn: function () {
      const names = ["Charlotte","Claire","Pascal","Lucas","Ludovic","Marion","Yves","Kyle","Hugo","Gaël","Kate"]
      var name = names[Math.floor(Math.random() * names.length)].concat("(",this.totalPatientsWelcomed,")")
      var newClient = new Step(name, 0, 15, this.totalPatientsWelcomed)
      this.totalPatientsWelcomed++
      this.patientsArrived.push(newClient)
    },
    patientRefused: function (id) {
      for (var i = 0; i < this.patientsArrived.length && this.patientsArrived[i].id != id; i++){
        continue;
      }
      
      if (i < this.patientsArrived.length) {
        this.patientsArrived.splice(i, 1)
      }
    },
    acceptPatient: function (id) {
      if (this.totalPatientsBeforeTreatment >= 5) {
        return false
      }
      
      for (var i = 0; i < this.patientsArrived.length && this.patientsArrived[i].id != id; i++){
        continue;
      }
      
      if (i < this.patientsArrived.length) {
        var patientWithPaperToFill = new Step(this.patientsArrived[i].nameOfClient, 5, 10, id)
        this.patientsArrived.splice(i, 1)
        this.totalPatientsBeforeTreatment++
        this.paperworkToFill.push(patientWithPaperToFill)
        return true
      }

      return false
    },
    fillsPaperwork: function (id) {
      for (var i = 0; i < this.paperworkToFill.length && this.paperworkToFill[i].id != id; i++){
        continue;
      }
      
      if (i < this.paperworkToFill.length) {
        var patientWithPaperToFill = new Step(this.paperworkToFill[i].nameOfClient, 5, 10, id)
        this.paperworkToFill.splice(i, 1)
        this.paperworkFilled.push(patientWithPaperToFill)
      }
    },
    processPaperwork: function (id) {
      for (var i = 0; i < this.paperworkFilled.length && this.paperworkFilled[i].id != id; i++){
        continue;
      }
      
      if (i < this.paperworkFilled.length && this.nursesAvailable > 0) {
        var patient = new Step(this.paperworkFilled[i].nameOfClient, 0, 9999, id)
        this.paperworkFilled.splice(i, 1)
        this.nursesAvailable--
        this.paperworkProcessFinished.push(patient)
      }
    },
    goesInEmergencyRoom: function (id) {
      for (var i = 0; i < this.paperworkProcessFinished.length && this.paperworkProcessFinished[i].id != id; i++){
        continue;
      }
      
      if (i < this.paperworkProcessFinished.length && this.roomsAvailable > 0) {
        var patient = new Step(this.paperworkProcessFinished[i].nameOfClient, 0, 99999, id)
        this.paperworkProcessFinished.splice(i, 1)
        this.roomsAvailable--
        this.nursesAvailable++
        this.patientsWaitingInEmergencyRoom.push(patient)
      }
    },
    startTreatment: function (id) {
      for (var i = 0; i < this.patientsWaitingInEmergencyRoom.length && this.patientsWaitingInEmergencyRoom[i].id != id; i++){
        continue;
      }
      
      if (i < this.patientsWaitingInEmergencyRoom.length && this.physiciansAvailable > 0) {
        var patient = new Step(this.patientsWaitingInEmergencyRoom[i].nameOfClient, 20, 90, id)
        this.patientsWaitingInEmergencyRoom.splice(i, 1)
        this.totalPatientsBeforeTreatment--
        this.physiciansAvailable--
        this.patientsUnderTreatment.push(patient)
      }
    },
    treatmentFinished: function (id) {
      for (var i = 0; i < this.patientsUnderTreatment.length && this.patientsUnderTreatment[i].id != id; i++){
        continue;
      }
      
      if (i < this.patientsUnderTreatment.length) {
        var patient = new Step(this.patientsUnderTreatment[i].nameOfClient, 5, 10, id)
        this.patientsUnderTreatment.splice(i, 1)
        this.physiciansAvailable++
        this.roomsAvailable++
        this.totalPatientsHealed++
        this.patientsHealed.push(patient)
      }
    },
    patientChecksOut: function (id) {
      for (var i = 0; i < this.patientsHealed.length && this.patientsHealed[i].id != id; i++){
        continue;
      }
      
      if (i < this.patientsHealed.length) {
        this.patientsHealed.splice(i, 1)
      }
    },
    // The observed service asks for a room
    requestForARoom: function () {
      var newRequest = new RequestForRoom(true, 0)
      this.messagesAskingForRoom.push(newRequest)
    },
    // The observed service offers for a room
    offersARoom: function () {
      for (var i = 0; i < this.messagesAskingForRoom.length &&
        this.messagesAskingForRoom[i].isItFromYourService; i++){
        continue;
      }
      
      if (i < this.messagesAskingForRoom.length && this.roomsAvailable > 1) {
        this.messagesAskingForRoom.splice(i, 1)
        this.roomsAvailable--
      }
    },
    rejectDemandForRoom: function () {
      if (this.messagesAskingForRoom.length > 0) {
        this.messagesAskingForRoom.splice(0, 1)
      }
    },
    outsideAsksForARoom: function () {
      var newRequest = new RequestForRoom(false, 0)
      this.messagesAskingForRoom.push(newRequest)
    },
    outsideOffersARoom: function () {
      if (this.messagesAskingForRoom.length > 0) {
        if (this.messagesAskingForRoom[0].isItFromYourService) {
          this.roomsAvailable++
          this.youRequestedARoom = false
        }
        this.messagesAskingForRoom.splice(0, 1)
      }
    },
    // The observed service asks for a physician
    requestFormAPhysician: function () {
      var newRequest = new RequestForPhysician(true, 0)
      this.messagesAskingForPhysicians.push(newRequest)
    },
    // The observed service offers for a physician
    offersAPhysician: function () {
      for (var i = 0; i < this.messagesAskingForPhysicians.length &&
        this.messagesAskingForPhysicians[i].isItFromYourService; i++){
        continue;
      }
      
      if (i < this.messagesAskingForPhysicians.length && this.physiciansAvailable > 1) {
        this.messagesAskingForPhysicians.splice(i, 1)
        this.physiciansAvailable--
      }
    },
    rejectDemandForPhysician: function () {
      if (this.messagesAskingForPhysicians.length > 0) {
        this.messagesAskingForPhysicians.splice(0, 1)
      }
    },
    outsideAsksForAPhysician: function () {
      var newRequest = new RequestForPhysician(false, 0)
      this.messagesAskingForPhysicians.push(newRequest)
    },
    outsideOffersAPhysician: function () {
      if (this.messagesAskingForPhysicians.length > 0) {
        if (this.messagesAskingForPhysicians[0].isItFromYourService) {
          this.physiciansAvailable++
          this.youRequestedAPhysician = false
        }
        this.messagesAskingForPhysicians.splice(0, 1)
      }
    },
    addASecond: function () {
      // For each list, add a second on all the Step elements in all the lists, if the maximum time reached 0,
      // the default action is executed
      this.addSecondOnPatientArrived()
      this.addSecondOnFillsPapework()
      this.addSecondOnProcessPaperwork()
      this.addSecondOnGoesInEmergency()
      this.addSecondOnStartTreatment()
      this.addSecondOnProceedTreatment()
      this.addSecondOnChecksOut()
    },
    addSecondOnPatientArrived: function () {
      this.patientsArrived.forEach(element => {
        element.minTime = Math.max(0, element.minTime - 1)
        element.maxTime = Math.max(0, element.maxTime - 1)
        
        if (element.maxTime === 0){
          if(!this.acceptPatient(element.id)){
            this.patientRefused(element.id)
          }
        }
        else if (element.minTime === 0 && Math.round(Math.random()) === 1) {
          if(!this.acceptPatient(element.id)){
            this.patientRefused(element.id)
          }
        }
      })
    },
    addSecondOnFillsPapework: function () {
      this.paperworkToFill.forEach(element => {
        element.minTime = Math.max(0, element.minTime - 1)
        element.maxTime = Math.max(0, element.maxTime - 1)
        
        if (element.maxTime === 0){
          this.fillsPaperwork(element.id)
        }
        else if (element.minTime === 0 && Math.round(Math.random()) === 1) {
          this.fillsPaperwork(element.id)
        }
      })
    },
    addSecondOnProcessPaperwork: function () {
      var nurses = this.nursesAvailable
      this.paperworkFilled.forEach(element => {
        if (nurses > 0) {
          element.minTime = Math.max(0, element.minTime - 1)
          element.maxTime = Math.max(0, element.maxTime - 1)
          nurses--
        }
        
        if (element.maxTime === 0) {
          this.processPaperwork(element.id)
        }
        else if (element.minTime === 0 && Math.round(Math.random()) === 1) {
          this.processPaperwork(element.id)
        }
      })
    },
    addSecondOnGoesInEmergency: function () {
      this.paperworkProcessFinished.forEach(element => {
        if (this.roomsAvailable > 0) {
          this.goesInEmergencyRoom(element.id)
        }
      })
    },
    addSecondOnStartTreatment: function () {
      this.patientsWaitingInEmergencyRoom.forEach(element => {
        if (this.physiciansAvailable > 0) {
          this.startTreatment(element.id)
        }
      })
    },
    addSecondOnProceedTreatment: function () {
      this.patientsUnderTreatment.forEach(element => {
        element.minTime = Math.max(0, element.minTime - 1)
        element.maxTime = Math.max(0, element.maxTime - 1)
        
        if (element.maxTime === 0){
          this.treatmentFinished(element.id)
        }
        else if (element.minTime === 0 && Math.round(Math.random() * 4) === 1) {
          this.treatmentFinished(element.id)
        }
      })
    },
    addSecondOnChecksOut: function () {
      this.patientsHealed.forEach(element => {
        element.minTime = Math.max(0, element.minTime - 1)
        element.maxTime = Math.max(0, element.maxTime - 1)
        
        if (element.maxTime === 0){
          this.patientChecksOut(element.id)
        }
        else if (element.minTime === 0 && Math.round(Math.random()) === 1) {
          this.patientChecksOut(element.id)
        }
      })
    },
    launchAutonomousSystem: function () {
      if (this.totalPatientsBeforeTreatment === 0) {
        this.offersARoom()
        this.offersAPhysician()
      }

      if (!this.youRequestedARoom &&
        this.paperworkProcessFinished.length - this.roomsAvailable >= 3) {
        this.requestForARoom()
        this.youRequestedARoom = true
      }

      if (!this.youRequestedAPhysician &&
        this.patientsWaitingInEmergencyRoom.length - this.physiciansAvailable >= 3) {
        this.requestFormAPhysician()
        this.youRequestedAPhysician = true
      }

      if (Math.round(Math.random() * 5) === 1) {
        this.patientComesIn()
      }
      
      if (Math.round(Math.random() * 20) === 1) {
        this.outsideAsksForARoom()
      }
      
      if (Math.round(Math.random() * 20) === 1) {
        this.outsideAsksForAPhysician()
      }
      
      if (this.messagesAskingForRoom.length > 1 && Math.round(Math.random() * 5) === 1) {
        this.outsideOffersARoom()
      }
      
      if (this.messagesAskingForPhysicians.length > 1 && Math.round(Math.random() * 5) === 1) {
        this.outsideOffersAPhysician()
      }

      this.addASecond()
      
      setTimeout(this.launchAutonomousSystem, 500)
    }
  }
}

class RequestForRoom {
  constructor(isItFromYourService, timeWaited){
    this.isItFromYourService = isItFromYourService
    this.timeWaited = timeWaited
  }
}

class RequestForPhysician {
  constructor(isItFromYourService, timeWaited){
    this.isItFromYourService = isItFromYourService
    this.timeWaited = timeWaited
  }
}


class Step {
  constructor(nameOfClient, minTime, maxTime, id){
    this.nameOfClient = nameOfClient
    this.maxTime = maxTime
    this.minTime = minTime
    this.id = id
  }
}
</script>

<style>
.displayInfo {
  display: inline-block;
  padding-right: 5px;
}

table,
td {
    border: 1px solid rgba(0, 0, 0, 0.431);
}
thead,
tfoot {
    background-color: rgba(4, 251, 37, 0.294);
    color: rgb(0, 0, 0);
}
</style>
