<template>
    <div id="secure">
        <div id="information">
            <h1>You</h1>
            <p>
                {{ firstName }} {{ lastName }} {{ shRanking }} {{ dhRanking }} {{ dmRanking }} {{ licenseId }}
            </p>
        </div>

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
                        {{ tournament.name }}
                        <button v-on:click="register(tournament.name)">Register to this tournament</button>
                        <div v-if="tournament.participation">
                            <input type="checkbox" id='SH' value=true v-model="participationChoices.SH">
                            <label for="SH">SH</label>
                            <input type="checkbox" id="DH" value=true v-model="participationChoices.DH">
                            <label for="DH">DH</label>
                            <input type="checkbox" id="DM" value=true v-model="participationChoices.DM">
                            <label for="DM">DM</label>
                            <button v-on:click="addParticipationChoices(tournament.name)">OK</button>
                        </div>
                        <div v-else>
                        </div>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Secure',
        data() {
            return {
                firstName: 'Romain',
                lastName: 'GIRO',
                shRanking: 'D8',
                dhRanking: 'D8',
                dmRanking: 'R6',
                licenseId: '00498401',
                success: false,
                tournamentToAdd: '',
                participationChoices: {
                    SH: false,
                    DH: false,
                    DM: false
                },
                tournamentList: []
            };
        },
        methods: {
            tournamentName() {
                this.success = true
            },
            addTournament() {
                this.tournamentList.push({ name: this.tournamentToAdd, participation: false, SH: '', DH: '', DM: '' })
            },
            register(tournamentName) {
                for (var i = 0; i<this.tournamentList.length; i++){
                    if(this.tournamentList[i].name == tournamentName) {
                        this.tournamentList[i].participation = true
                    }
                }
            },
            addParticipationChoices(tournamentName) {
                for (var i = 0; i<this.tournamentList.length; i++){
                    if(this.tournamentList[i].name == tournamentName) {
                        if(this.participationChoices.SH == true){
                            this.tournamentList[i].SH = 'OK'
                            this.participationChoices.SH = false
                        }
                        if(this.participationChoices.DH == true){
                            this.tournamentList[i].DH = 'OK'
                            this.participationChoices.DH = false
                        }
                        if(this.participationChoices.DM == true){
                            this.tournamentList[i].DM = 'OK'
                            this.participationChoices.DM = false
                        }
                    }
                }
                console.log(this.tournamentList)
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
</style>