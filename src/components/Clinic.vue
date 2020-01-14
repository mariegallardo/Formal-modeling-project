<template>
  <div>
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
    <button v-on:click="patientComesIn">Patients comes in</button>
    <input v-model="clientToRefuse">
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
    <button v-on:click="requestFormAPhysician">Request for a physician</button>
    <button v-on:click="offersAPhysician">Offers a physician</button>
    <button v-on:click="outsideAsksForAPhysician">Outside asks for a physician</button>
    <button v-on:click="outsideOffersAPhysician">Outside offers a physician</button>
    <button v-on:click="rejectDemandForPhysician">Reject demand for a physician</button>
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
      totalPatientsWelcomed: 0
    }
  },
  methods: {
    patientComesIn: function () {
      var newClient = new Step("anonymous", 0, 15, this.totalPatientsWelcomed)
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
      }
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
        var patient = new Step(this.paperworkFilled[i].nameOfClient, 5, 10, id)
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
        var patient = new Step(this.paperworkProcessFinished[i].nameOfClient, 5, 10, id)
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
        var patient = new Step(this.patientsWaitingInEmergencyRoom[i].nameOfClient, 5, 10, id)
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
      this.messagesAskingForRoom++
    },
    // The observed service offers for a room
    offersARoom: function () {
      if (this.messagesAskingForRoom > 0 && this.roomsAvailable > 0) {
        this.messagesAskingForRoom--
        this.roomsAvailable--
      }
    },
    rejectDemandForRoom: function () {
      if (this.messagesAskingForRoom > 0) {
        this.messagesAskingForRoom--
      }
    },
    outsideAsksForARoom: function () {
      this.messagesAskingForRoom++
    },
    outsideOffersARoom: function () {
      if (this.messagesAskingForRoom > 0) {
        this.messagesAskingForRoom--
        this.roomsAvailable++
      }
    },
    // The observed service asks for a physician
    requestFormAPhysician: function () {
      this.messagesAskingForPhysicians++
    },
    // The observed service offers for a physician
    offersAPhysician: function () {
      if (this.messagesAskingForPhysicians > 0 && this.physiciansAvailable > 0) {
        this.messagesAskingForPhysicians--
        this.physiciansAvailable--
      }
    },
    rejectDemandForPhysician: function () {
      if (this.messagesAskingForPhysicians > 0) {
        this.messagesAskingForPhysicians--
      }
    },
    outsideAsksForAPhysician: function () {
      this.messagesAskingForPhysicians++
    },
    outsideOffersAPhysician: function () {
      if (this.messagesAskingForPhysicians > 0) {
        this.messagesAskingForPhysicians--
        this.physiciansAvailable++
      }
    }
  }
}

/*class RequestForRoom {
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
}*/


class Step {
  constructor(nameOfClient, minDuration, maxDuration, id){
    this.nameOfClient = nameOfClient
    this.maxTime = maxDuration
    this.minTime = minDuration
    this.id = id
  }
}
</script>

<style>
.displayInfo {
  display: inline-block;
  padding-right: 5px;
}
</style>
