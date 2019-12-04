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
                <button v-on:click="tournamentName">Add a tournament</button>
                <div v-if="success">
                    <input type="text" v-model="tournamentToAdd" v-on:keyup.enter="addTournament">
                </div>
            </div>
            <div>
                <ul>
                    <li v-for="item in items">
                        {{ item }}
                        <button v-on:click="register">Register to this tournament</button>
                        <div v-if="registerSuccess">
                            <input type="text" v-model="tournamentCategory1">
                            <input type="text" v-model="tournamentCategory2">
                            <input type="text" v-model="tournamentCategory3">
                            <button v-on:click="addRegistration">Add registration</button>
                        </div>
                        <div v-else>
                        </div>
                        <p v-if="registered">registered</p>
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
                registerSuccess: false,
                registerd: false,
                tournamentToAdd: '',
                items: [],
                tournamentCategory1: '',
                tournamentCategory2: '',
                tournamentCategory3: '',
                tournaments: [],
            };
        },
        methods: {
            tournamentName() {
                this.success = true
            },
            addTournament() {
                this.items.push(this.tournamentToAdd)
            },
            register() {
                this.registerSuccess = true
            },
            addRegistration() {
                this.tournaments.push([this.tournamentCategory1, this.tournamentCategory2, this.tournamentCategory3])
                this.registered = true
                this.registerSuccess = false
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