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
                            <p>participe</p>
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
                tournamentList: [],
            };
        },
        methods: {
            tournamentName() {
                this.success = true
            },
            addTournament() {
                this.tournamentList.push({ name: this.tournamentToAdd, participation: false })
            },
            register(tournamentName) {
                console.log(tournamentName)
                for (var i = 0; i<this.tournamentList.length; i++){
                    if(this.tournamentList[i].name == tournamentName) {
                        this.tournamentList[i].participation = true
                    }
                }
            },
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