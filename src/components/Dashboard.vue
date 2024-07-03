<template>
    <table>
        <thead>
            <tr>
                <th>#</th>
                <th>Cliente</th>
                <th>Pão</th>
                <th>Carne</th>
                <th>Opcionais</th>
                <th>Ações</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="burger in burgers" :key="burger.id">
                <td class="id">{{ burger.id }}</td>
                <td>{{ burger.name }}</td>
                <td>{{ burger.bread }}</td>
                <td>{{ burger.meat }}</td>
                <td>
                    <ul>
                        <li v-for="(optional, index) in burger.optionals" :key="index">{{ optional }}</li>
                    </ul>
                </td>
                <td>
                    <select name="status" @change="updateBurger($event, burger.id)">
                        <option
                            v-for="statusItem in status"
                            :key="statusItem.id"
                            :value="statusItem.type"
                            :selected="burger.status === statusItem.type"
                        >
                            {{ statusItem.type }}
                        </option>
                    </select>
                    <button @click="deleteBurger(burger.id)">Cancelar</button>
                </td>
            </tr>
        </tbody>
    </table>
    <Message :msg="msg" v-show="msg" />
</template>

<script>
import Message from "@/components/Message.vue";

export default {
    name: "Dashboard",
    components: {
        Message,
    },
    data() {
        return {
            burgers: null,
            status: [],
            msg: null,
        };
    },
    methods: {
        async getBurgers() {
            const req = await fetch("http://localhost:3000/burgers");
            const data = await req.json();
            this.burgers = data;

            this.getStatus();
        },

        async getStatus() {
            const req = await fetch("http://localhost:3000/status");
            const data = await req.json();
            this.status = Array.from(data);
        },

        async deleteBurger(id) {
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "DELETE",
            });

            const res = await req.json();
            this.msg = `Pedido Nº ${res.id} deletado com sucesso`;
            setTimeout(() => (this.msg = ""), 3000);

            this.getBurgers();
        },

        async updateBurger(event, id) {
            const option = event.target.value;
            const dataJson = JSON.stringify({ status: option });

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "PATCH",
                headers: { "Content-type": "application/json" },
                body: dataJson
            });

            const res = await req.json();

            this.msg = `Pedido Nº ${res.id} atualizado com sucesso`;
            setTimeout(() => (this.msg = ""), 3000);
        },
    },
    mounted() {
        this.getBurgers();
    },
};
</script>

<style lang="less" scoped>
table {
    width: 1200px;
    margin: 0 auto;
    border-collapse: collapse;

    thead {
        font-weight: bold;

        th {
            border-bottom: 3px solid #333;
            padding: 12px;
            text-align: start;
        }
    }

    tbody {
        td {
            border-bottom: 1px solid #ccc;
            padding: 12px;
            width: 19%;

            &.id {
                width: 5%;
            }

            select {
                padding: 12px 2px;
                margin-right: 6px;
            }

            button {
                background-color: #222;
                color: #fcba03;
                font-weight: bold;
                border: 2px solid #222;
                padding: 10px;
                font-size: 16px;
                cursor: pointer;
                transition: 0.5s;

                &:hover {
                    background: transparent;
                    color: #222;
                }
            }
        }
    }
}
</style>
