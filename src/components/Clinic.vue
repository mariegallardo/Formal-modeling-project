<template>

  <div>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
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
    <aside>
      <table>
        <thead>
          <tr>
            <th>Current time</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>{{minutes}}</td>
          </tr>
        </tbody>
      </table>
      <br/>
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
          <tr>
            <td>Total number of rooms:{{totalOfRooms}}</td>
          </tr>
          <tr>
            <td>Total number of physicians:{{totalOfPhysicians}}</td>
          </tr>
        </tbody>
      </table>
      <br/>
      <table>
        <thead>
          <tr>
            <th>total patients before treatment</th>
            </tr>
        </thead>
        <tbody>
          <tr>
            <td>{{totalPatientsBeforeTreatment}}</td>
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
    </aside>
    
    <section>
    <table>
      <thead>
        <tr>
          <th>patient comes in</th>
          <th>patient fills the paperwork</th>
          <th>paperwork filled</th>
          <th>paperwork processed by nurse finished</th>
          <th>patients waiting in emergency room</th>
          <th>patients under treatment</th>
          <th>patients is healed waiting for checkout</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>
            <li v-for="item in patientsArrived" :key="item.nameOfClient">
              {{ item.nameOfClient }}-[{{item.minTime}},{{item.maxTime}}]
            </li>
          </td>
          <td>
            <li v-for="item in paperworkToFill" :key="item.nameOfClient">
              {{ item.nameOfClient }}-[{{item.minTime}},{{item.maxTime}}]
            </li>
          </td>
          <td>
            <li v-for="item in paperworkFilled" :key="item.nameOfClient">
              {{ item.nameOfClient }}-[{{item.minTime}},{{item.maxTime}}]
            </li>
          </td>
          <td>
            <li v-for="item in paperworkProcessFinished" :key="item.nameOfClient">
              {{ item.nameOfClient }}-[{{item.minTime}},{{item.maxTime}}]
            </li>
          </td>
          <td>
            <li v-for="item in patientsWaitingInEmergencyRoom" :key="item.nameOfClient">
              {{ item.nameOfClient }}-[{{item.minTime}},{{item.maxTime}}]
            </li>
          </td>
          <td>
            <li v-for="item in patientsUnderTreatment" :key="item.nameOfClient">
              {{ item.nameOfClient }}-[{{item.minTime}},{{item.maxTime}}]
            </li>
          </td>
          <td>
            <li v-for="item in patientsHealed" :key="item.nameOfClient">
              {{ item.nameOfClient }}-[{{item.minTime}},{{item.maxTime}}]
            </li>
          </td>
        </tr>
      </tbody>
    </table>
    </section>
    <aside>
    <h3>Automatic</h3>
    <button v-on:click="launchAutonomousSystem">Launch system</button>
    </aside>
    <br/>
    <table>
      <thead>
        <tr>
          <th class="minWidth">Messages asking for a room</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>
            <li v-for="item in messagesAskingForRoom" :key="item.isItFromYourService">
              room request <div v-if="item.isItFromYourService===true">from your service</div> {{item.timeWaited}} m ago
            </li>
          </td>
        </tr>
      </tbody>
    </table>
    <br/>
    <table>
      <thead>
        <tr>
          <th class="minWidth">Messages asking for a physicians</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>
            <li v-for="item in messagesAskingForPhysicians" :key="item.isItFromYourService">
              physician request <div v-if="item.isItFromYourService===true">from your service</div> {{item.timeWaited}} m ago
            </li>
          </td>
        </tr>
      </tbody>
    </table>
    <br/>
    <h3>Manual</h3>
    <table>
      <thead>
        <tr>
          <th>change time</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><button v-on:click="addAMinute">Add a minute</button></td>
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
        <tr>
          <th colspan="2">Inside</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><button v-on:click="requestForARoom">Request for a room</button></td>
          <td><button v-on:click="offersARoom">Offers a room</button></td>
        </tr>
        <tr>
          <td><button v-on:click="requestForAPhysician">Request for a physician</button></td>
          <td><button v-on:click="offersAPhysician">Offers a physician</button></td>
          
        </tr>
      </tbody>
    </table>
    <br/>
    <table>
      <thead>
        <tr>
          <th colspan="2">Outside</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><button v-on:click="outsideAsksForARoom">Outside asks for a room</button></td>
          <td><button v-on:click="outsideOffersARoom">Outside offers a room</button></td>
        </tr>
        <tr>
          <td><button v-on:click="outsideAsksForAPhysician">Outside asks for a physician</button></td>
          <td><button v-on:click="outsideOffersAPhysician">Outside offers a physician</button></td>
        </tr>
      </tbody>
    </table>
    <br/>
    <table>
      <thead>
        <tr>
          <th colspan="2">Reject outside requests</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><button v-on:click="rejectDemandForRoom">Reject demand for a room</button></td>
          <td><button v-on:click="rejectDemandForPhysician">Reject demand for a physician</button></td>
        </tr>
      </tbody>
    </table>
    <!--
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
    <button v-on:click="rejectDemandForPhysician">Reject demand for a physician</button>
    <br/>
    <button v-on:click="addAMinute">Add a minute</button>
    -->
    
  </div>
</template>

<script>
export default {
  name: 'clinic',
  data: function () {
    return {
      minutes:0, // the time counter of the system
      patientsArrived: [], // the list of patients which comes to the service
      paperworkToFill: [], // the list of patients which are accepeted and need to fill paperwork
      paperworkFilled: [], // the list of patients that have filled the paperwork and need to wait a nurse to process the paperwork
      paperworkProcessFinished: [], // the list of the patients for whom the nurses have processed the paperwork
      patientsWaitingInEmergencyRoom: [], // the list of the patients that are waiting in an emergency room 
      patientsUnderTreatment: [], // the list of the patients that are currently treated by a physician in a room
      patientsHealed: [], // the patient that have been healed and are going to checkout, the physician and the room becomes available when the patient under this step
      nursesAvailable: 5, // the counter of available nurses
      roomsAvailable: 5,  // the counter of available rooms
      physiciansAvailable: 5, // the counter of available physicians
      totalOfRooms:5, // the total number of rooms in the service, this number changes if the service asks or offers a room
      totalOfPhysicians:5, // the total number of physicians in the service this number changes if the service if the service asks or offers a physician
      totalOfNurses:5, // the total number of nurses in the service, this number is a constant
      totalPatientsBeforeTreatment: 0, // the total number of patients that have been accepted but are waiting to be treated
      totalPatientsWelcomed: 0, // the total number of patients coming in the service 
      totalPatientsHealed:0, // the total number of patients that have been healed
      messagesAskingForRoom: [], // the buffer b0 where the requests for rooms transit
      messagesAskingForPhysicians: [], // the buffer b1 where the requests for physicians transit
      clientToRefuse: -1,
      youRequestedARoom: false,
      youRequestedAPhysician: false
    }
  },
  methods: {
    patientComesIn: function () {
      const names = ["Claire","Pascal","Lucas","Ludo","Mario","Yves","Kyle","Hugo","Gaël","Kate","Lucie","Théa","Mia","Lou","Zoé","Eva","Nina"]
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
        if(this.patientsArrived.minTime > 0){
          return
        }
        this.patientsArrived.splice(i, 1)
      }
    },
    acceptPatient: function (id) {
      if (this.totalPatientsBeforeTreatment >= Math.min(this.totalOfPhysicians,this.totalOfRooms, 2 * this.totalOfNurses)) {
        return false
      }
      
      for (var i = 0; i < this.patientsArrived.length && this.patientsArrived[i].id != id; i++){
        continue;
      }
      
      if (i < this.patientsArrived.length) {
        if(this.patientsArrived.minTime > 0){
          return
        }
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
        if(this.paperworkToFill[i].minTime > 0){
          return
        }
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
        if(this.paperworkFilled[i].minTime > 0){
          return
        }
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
        if(this.paperworkProcessFinished[i].minTime > 0){
          return
        }
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
        if(this.patientsWaitingInEmergencyRoom[i].minTime > 0){
          return
        }
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
        if(this.patientsUnderTreatment[i].minTime > 0){
          return
        }
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
        if(this.patientsHealed[i].minTime > 0){
          return
        }
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
        this.totalOfRooms--
      }
    },
    rejectDemandForRoom: function () {
      if (this.messagesAskingForRoom.length > 0) {
        if (this.messagesAskingForRoom[0].isItFromYourService) {
          this.youRequestedARoom = false
        }
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
          this.totalOfRooms++
          this.youRequestedARoom = false
        }
        this.messagesAskingForRoom.splice(0, 1)
      }
    },
    // The observed service asks for a physician
    requestForAPhysician: function () {
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
        this.totalOfPhysicians--
      }
    },
    rejectDemandForPhysician: function () {
      if (this.messagesAskingForPhysicians.length > 0) {
        if (this.messagesAskingForPhysicians[0].isItFromYourService) {
          this.youRequestedAPhysician = false
        }
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
          this.totalOfPhysicians++
          this.youRequestedAPhysician = false
        }
        this.messagesAskingForPhysicians.splice(0, 1)
      }
    },
    addAMinute: function () {
      this.minutes++
      // For each list, add a minute on all the Step elements in all the lists, if the maximum time reached 0,
      // the default action is executed
      this.addMinuteOnPatientArrived()
      this.addMinuteOnFillsPapework()
      this.addMinuteOnProcessPaperwork()
      this.addMinuteOnGoesInEmergency()
      this.addMinuteOnStartTreatment()
      this.addMinuteOnProceedTreatment()
      this.addMinuteOnChecksOut()
      this.addMinuteToRequests()
    },
    addMinuteToRequests: function () {
      for(var i=0; i<this.messagesAskingForRoom.length;i++){
        this.messagesAskingForRoom[i].timeWaited++
        if(this.messagesAskingForRoom[i].timeWaited >= 60){
          this.messagesAskingForRoom.splice(i,1)
        }
      }
      for(i=0; i<this.messagesAskingForPhysicians.length;i++){
        this.messagesAskingForPhysicians[i].timeWaited++
        if(this.messagesAskingForPhysicians[i].timeWaited >= 60){
          this.messagesAskingForPhysicians.splice(i,1)
        }
      }


    },
    addMinuteOnPatientArrived: function () {
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
    addMinuteOnFillsPapework: function () {
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
    addMinuteOnProcessPaperwork: function () {
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
    addMinuteOnGoesInEmergency: function () {
      this.paperworkProcessFinished.forEach(element => {
        if (this.roomsAvailable > 0) {
          this.goesInEmergencyRoom(element.id)
        }
      })
    },
    addMinuteOnStartTreatment: function () {
      this.patientsWaitingInEmergencyRoom.forEach(element => {
        if (this.physiciansAvailable > 0) {
          this.startTreatment(element.id)
        }
      })
    },
    addMinuteOnProceedTreatment: function () {
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
    addMinuteOnChecksOut: function () {
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
        this.requestForAPhysician()
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

      this.addAMinute()
      
      setTimeout(this.launchAutonomousSystem, 500)
    }
  }
}

// represent any request for a room that transit into b0
class RequestForRoom {
  constructor(isItFromYourService, timeWaited){
    this.isItFromYourService = isItFromYourService // a boolean to know if the request was from the service
    this.timeWaited = timeWaited // a counter to know how much time has past since the request was emitted
  }
}
// represent any request for a physician that transit into b1
class RequestForPhysician {
  constructor(isItFromYourService, timeWaited){
    this.isItFromYourService = isItFromYourService // a bolean to know if the request was from the service
    this.timeWaited = timeWaited // a counter to know how much time has past since the request was emitted
  }
}
// represent the a client in a step (patient comes in,	patient fills the paperwork,	paperwork filled, ... )
class Step {
  constructor(nameOfClient, minTime, maxTime, id){
    this.nameOfClient = nameOfClient // the name of the patient
    this.maxTime = maxTime  // the maximum time amount of time the patient should wait in this step, if the maxTime == 0 then the patient should go to the next step or leave the service
    this.minTime = minTime  // the minimum amount of time the the patient should wait in this step, if the minTime <= 0 then the patient can go to the next step, but if the minTime >= 0 then the patient cannot go to the next step
    this.id = id // the id of the client
  }
}
</script>

<style>
.displayInfo {
  display: inline-block;
  padding-right: 5px;
}
aside {
  padding-left:1%;
  float: right;
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

#minWidth{
  min-width:100px;
}
</style>
