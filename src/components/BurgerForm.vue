<template>
    <div>
        <form @submit="createBurger">
            <div class="input-container">
                <label for="name" class="title">Nome:</label>
                <input type="text" id="name" name="name" v-model="name" placeholder="Digite o seu nome" />
            </div>

            <div class="input-container">
                <label for="bread" class="title">Escolha o pão:</label>
                <select name="bread" id="bread" v-model="bread">
                    <option value="null">Selecione o seu pão</option>
                    <option v-for="bread in breadsData" :key="bread.id" :value="bread.type">{{ bread.type }}</option>
                </select>
            </div>

            <div class="input-container">
                <label for="meat" class="title">Escolha a carne:</label>
                <select name="meat" id="meat" v-model="meat">
                    <option value="null">Selecione a sua carne</option>
                    <option v-for="meat in meatsData" :key="meat.id" :value="meat.type">{{ meat.type }}</option>
                </select>
            </div>

            <div id="optionals-container" class="input-container">
                <label for="optionals" class="title">Selecione os opcionais:</label>
                <label class="checkbox-container" v-for="optional in optionalsData" :key="optional.id">
                    <input type="checkbox" name="optionals" v-model="optionals" :value="optional.type" />
                    <span>{{ optional.type }}</span>
                </label>
            </div>

            <div class="input-container">
                <input type="submit" value="Criar meu Burger!" />
            </div>
        </form>
        <Message :msg="msg" v-show="msg" />
    </div>
</template>

<script>
import Message from "@/components/Message.vue";

export default {
    name: "BurgerForm",
    components: {
        Message,
    },
    data() {
        return {
            breadsData: null,
            meatsData: null,
            optionalsData: null,
            name: null,
            bread: null,
            meat: null,
            optionals: [],
            status: "Solicitado",
            msg: null,
        };
    },
    methods: {
        async getIngredients() {
            const req = await fetch("http://localhost:3000/ingredients");
            const data = await req.json();

            this.breadsData = data.breads;
            this.meatsData = data.meats;
            this.optionalsData = data.optionals;
        },
        async createBurger(e) {
            e.preventDefault();

            const data = {
                name: this.name,
                meat: this.meat,
                bread: this.bread,
                optionals: Array.from(this.optionals),
                status: this.status,
            };

            const dataJson = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson,
            });

            const res = await req.json();

            this.msg = `Pedido Nº ${res.id} realizado com sucesso`;
            setTimeout(() => (this.msg = ""), 3000);

            this.name = "";
            this.meat = "";
            this.bread = "";
            this.optionals = "";
        },
    },
    mounted() {
        this.getIngredients();
    },
};
</script>

<style lang="less" scoped>
div {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;

    form {
        width: 400px;

        .input-container {
            display: flex;
            flex-direction: column;
            margin-bottom: 20px;

            .title {
                width: 100%;
                font-weight: bold;
                margin-bottom: 15px;
                color: #222;
                padding: 5px 10px;
                border-left: 4px solid #fcba03;
            }

            input,
            select {
                padding: 5px 10px;
                width: 100%;
            }

            input[type="submit"] {
                background: #222;
                color: #fcba03;
                font-weight: bold;
                border: 2px solid #222;
                padding: 10px;
                font-size: 16px;
                cursor: pointer;
                transition: 0.5;
            }
        }

        #optionals-container {
            flex-direction: row;
            flex-wrap: wrap;

            label {
                width: 100%;
            }

            .checkbox-container {
                display: flex;
                align-items: flex-start;
                width: 50%;
                margin-bottom: 20px;

                span,
                input {
                    width: auto;
                }

                span {
                    margin-left: 6px;
                    font-weight: bold;
                }
            }
        }
    }
}
</style>
