<template>
    <div id="secure">
        <div id="information">
            <h1>You</h1>
            <p>
                {{ firstName }} {{ lastName }} {{ shRanking }} {{ dhRanking }} {{ dmRanking }} {{ licenseId }}
            </p>
            <p> Number of inscriptions : {{ numberOfInscription }} </p>
        </div>

        <div>
            <div :id="showTournament ? 'tournamentLeft' : '' ">
                <div id="tournamentList">
                    <h1>Tournament List</h1>
                    <div>

                        <button @click="tournamentName">Add a tournament</button>

                        <div v-if="success">
                            <input type="text" v-model="tournamentToAdd" v-on:keyup.enter="addTournament">
                        </div>

                    </div>
                    <div>
                        <ul>
                            <li v-for="tournament in tournamentList">

                                <p v-on:click="showTournamentInformation(tournament.name)">{{ tournament.name }}</p>

                                <button v-if="!tournament.participation" v-on:click="register(tournament.name)">Register to this tournament</button>
                                <button v-else v-on:click="remove(tournament.name)">Remove from this tournament</button>

                                <div v-if="tournament.participation">

                                    <input type="checkbox" id='SH' v-on:click="addSingleChoice(tournament.name)">
                                    <label for="SH">SH</label>

                                    <input type="checkbox" id='DH' v-on:click="addDoubleChoice(tournament.name)">
                                    <label for="DH">DH</label>

                                    <input type="checkbox" id='DM' v-on:click="addMixedChoice(tournament.name)">
                                    <label for="DM">DM</label>

                                </div>

                                <div v-else>
                                </div>

                            </li>
                        </ul>
                    </div>
                </div>
            </div>

            <div v-if="showTournament" :id="showTournament ? 'tournamentRight' : '' ">
                <table>
                    <tr>
                        <td>date</td>
                        <td>{{ tournamentInformation.date }}</td>
                    </tr>

                    <tr>
                        <td>address</td>
                        <td>{{ tournamentInformation.address }}</td>
                    </tr>

                    <tr>
                        <td>players</td>
                        <td>
                            <ul id="tournamentInformation">
                                <li v-for="player in tournamentInformation.players">{{player}}</li>
                            </ul>
                        </td>
                    </tr>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Secure',
        data() {
            return {
                numberOfInscription: 0,
                firstName: 'Romain',
                lastName: 'GIRO',
                shRanking: 'D8',
                dhRanking: 'D8',
                dmRanking: 'R6',
                licenseId: '00498401',
                success: false,
                showTournament: false,
                tournamentToAdd: '',
                tournamentList: [],
                tournamentInformation: {
                    date: '',
                    address: '',
                    players: []
                }
            };
        },
        methods: {

            tournamentName() {
                this.success = true
            },

            addTournament() {
                this.tournamentList.push({
                    name: this.tournamentToAdd,
                    participation: false,
                    SH: 'NO',
                    DH: 'NO',
                    DM: 'NO',
                    date: 'JJ/MM/AAAA',
                    address: 'address',
                    players: ['Toto', 'Tata', 'Titi', 'Tutu']
                })
            },

            register(tournamentName) {
                for (var i = 0; i<this.tournamentList.length; i++){
                    if(this.tournamentList[i].name == tournamentName) {
                        this.tournamentList[i].participation = true
                        this.numberOfInscription++
                    }
                }
            },

            remove(tournamentName) {
                for (var i = 0; i<this.tournamentList.length; i++){
                    if(this.tournamentList[i].name == tournamentName) {
                        this.tournamentList[i].participation = false
                        this.tournamentList[i].SH = 'NO'
                        this.tournamentList[i].DH = 'NO'
                        this.tournamentList[i].DM = 'NO'
                        this.numberOfInscription--
                    }
                }
            },

            addSingleChoice(tournamentName) {
                for (var i = 0; i<this.tournamentList.length; i++){
                    if(this.tournamentList[i].name == tournamentName && this.tournamentList[i].SH === 'NO') {
                        this.tournamentList[i].SH = 'OK'
                    } else if (this.tournamentList[i].name == tournamentName && this.tournamentList[i].SH === 'OK') {
                        this.tournamentList[i].SH = 'NO'
                    }
                }
            },

            addDoubleChoice(tournamentName) {
                for (var i = 0; i<this.tournamentList.length; i++){
                    if(this.tournamentList[i].name == tournamentName && this.tournamentList[i].DH === 'NO') {
                        this.tournamentList[i].DH = 'OK'
                    } else if (this.tournamentList[i].name == tournamentName && this.tournamentList[i].DH === 'OK') {
                        this.tournamentList[i].DH = 'NO'
                    }
                }
            },

            addMixedChoice(tournamentName) {
                for (var i = 0; i<this.tournamentList.length; i++){
                    if(this.tournamentList[i].name == tournamentName && this.tournamentList[i].DM === 'NO') {
                        this.tournamentList[i].DM = 'OK'
                    } else if (this.tournamentList[i].name == tournamentName && this.tournamentList[i].DM === 'OK') {
                        this.tournamentList[i].DM = 'NO'
                    }
                }
            },

            showTournamentInformation(tournamentName) {
                for (var i = 0; i<this.tournamentList.length; i++){
                    if(this.tournamentList[i].name === tournamentName && this.showTournament === false){
                        this.showTournament = true
                        this.tournamentInformation.date = this.tournamentList[i].date
                        this.tournamentInformation.address = this.tournamentList[i].address
                        this.tournamentInformation.players = this.tournamentList[i].players
                    } else if (this.tournamentList[i].name === tournamentName && this.showTournament === true){
                        this.showTournament = false
                        this.tournamentInformation.date = ''
                        this.tournamentInformation.address = ''
                        this.tournamentInformation.players = ''
                    }
                }
            }
        }
    }
</script>

<style>
    #information {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        background-color: #FFFFFF;
        border: 1px solid #CCCCCC;
        padding: 20px;
        margin-top: 10px;
    }

    #tournamentList {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        background-color: #FFFFFF;
        padding: 20px;
        margin-top: 10px;
    }

    #tournamentLeft {
        float: left;
        text-align: center;
        padding-left: 200px;
        padding-top: 50px;
    }

    #tournamentRight {
        float: right;
        text-align: center;
        padding-right: 200px;
        padding-top: 150px;
    }

    ul {
        list-style-type: none;
        text-align: center;
        margin-left:0;
        padding-left:0;
    }

    table {
    width: 100%;
    }

    td, th {
    border: thin solid #000000;
    width: 50%;
    }
</style>