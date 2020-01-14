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
    <button v-on:click="patientRefused">Patient refused</button>
    <button v-on:click="acceptPatient">Accept patient</button>
    <button v-on:click="fillsPaperwork">Fills paperwork</button>
    <button v-on:click="processPaperwork">Process paperwork</button>
    <button v-on:click="goesInEmergencyRoom">Goes in emergenct room</button>
    <button v-on:click="startTreatment">Start treatment</button>
    <button v-on:click="treatmentFinished">Treatment finished</button>
    <button v-on:click="patientChecksOut">Patient checks out</button>
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
      patientsArrived: 0,
      paperworkToFill: 0,
      paperworkFilled: 0,
      paperworkProcessFinished: 0,
      patientsWaitingInEmergencyRoom: 0,
      patientsUnderTreatment: 0,
      patientsHealed: 0,
      nursesAvailable: 5,
      roomsAvailable: 5,
      physiciansAvailable: 5,
      messagesAskingForRoom: 0,
      messagesAskingForPhysicians: 0,
      totalPatientsBeforeTreatment: 0
    }
  },
  methods: {
    patientComesIn: function () {
      this.patientsArrived++
    },
    patientRefused: function () {
      if (this.patientsArrived > 0) {
        this.patientsArrived--
      }
    },
    acceptPatient: function () {
      if (this.totalPatientsBeforeTreatment >= 5) {
        return false;
      }
      
      this.patientsArrived--
      this.totalPatientsBeforeTreatment++
      this.paperworkToFill++
      return true
    },
    fillsPaperwork: function () {
      if (this.paperworkToFill > 0) {
        this.paperworkToFill--
        this.paperworkFilled++
      }
    },
    processPaperwork: function () {
      this.paperworkFilled--
      this.nursesAvailable--
      this.paperworkProcessFinished++
    },
    goesInEmergencyRoom: function () {
      this.paperworkProcessFinished--
      this.roomsAvailable--
      this.nursesAvailable++
      this.patientsWaitingInEmergencyRoom++
    },
    startTreatment: function () {
      this.totalPatientsBeforeTreatment--
      this.patientsWaitingInEmergencyRoom--
      this.physiciansAvailable--
      this.patientsUnderTreatment++
    },
    treatmentFinished: function () {
      this.patientsUnderTreatment--
      this.physiciansAvailable++
      this.roomsAvailable++
      this.patientsHealed++
    },
    patientChecksOut: function () {
      this.patientsHealed--
    },
    // The observed service asks for a room
    requestForARoom: function () {
      this.messagesAskingForRoom++
    },
    // The observed service offers for a room
    offersARoom: function () {
      this.messagesAskingForRoom--
      this.roomsAvailable--
    },
    rejectDemandForRoom: function () {
      this.messagesAskingForRoom--
    },
    outsideAsksForARoom: function () {
      this.messagesAskingForRoom++
    },
    outsideOffersARoom: function () {
      this.messagesAskingForRoom--
      this.roomsAvailable++
    },
    // The observed service asks for a physician
    requestFormAPhysician: function () {
      this.messagesAskingForPhysicians++
    },
    // The observed service offers for a physician
    offersAPhysician: function () {
      this.messagesAskingForPhysicians--
      this.physiciansAvailable--
    },
    rejectDemandForPhysician: function () {
      this.messagesAskingForPhysicians--
    },
    outsideAsksForAPhysician: function () {
      this.messagesAskingForPhysicians++
    },
    outsideOffersAPhysician: function () {
      this.messagesAskingForPhysicians--
      this.physiciansAvailable++
    }
  }
}
</script>

<style>
.displayInfo {
  display: inline-block;
  padding-right: 5px;
}
</style>
