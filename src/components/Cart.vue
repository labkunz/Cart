<template>
    <div>
        <a-row>
            <a-col>
                <h2> Products </h2>
            </a-col>
        </a-row>

        <a-row :gutter="32">
            <a-col v-for="product in products" :key="product.id" :span="24/products.length">
                <a-card>
                    <img
                        slot="cover"
                        :alt="product.name"
                        :src="require(`../assets/Switch${product.id}.png`)"
                        width="250"
                        height="250"
                    />

                    <a-card-meta :title="product.name">
                        <template slot="description">
                            price : ${{ product.price }}
                        </template>
                    </a-card-meta>

                    <a-button type="primary" @click="add(product)"> Add to Cart</a-button>
                </a-card>
            </a-col>
        </a-row>

        <a-row>
            <a-col>
                <h2> Cart </h2>
            </a-col>
        </a-row>

        <a-row>
            <a-col>
                <a-table 
                    v-show="cart.length > 0"
                    :columns="columns" 
                    :dataSource="cart" 
                    :rowKey="record => record.Id"
                    :pagination="{ hideOnSinglePage: true }"
                >

                    <template slot="#" slot-scope="data">
                        {{ data.id }}
                    </template>

                    <template slot="remove" slot-scope="data">
                        <a-button type="" @click="remove(data.id)"> Delete </a-button>
                    </template>

                    <template slot="good" slot-scope="data">
                        <img
                            :src="require(`../assets/Switch${data.id}.png`)"
                            width="50"
                            height="50"
                        />
                        {{ data.name }}
                    </template>

                    <template slot="quantity" slot-scope="data">
                        <a-row type="flex" justify="space-around" align="middle">
                            <a-col :span="8">
                                <a-button type="" @click="increase(data.id)"> + </a-button>
                            </a-col>
                            <a-col :span="8">
                                <a-input-number :value="data.quantity" />
                            </a-col>
                            <a-col :span="8">
                                <a-button type="" @click="decrease(data.id)"> - </a-button>
                            </a-col>
                        </a-row>
                    </template>

                    <template slot="price" slot-scope="data">
                        {{ data.price }}                        
                    </template>

                    <template slot="total" slot-scope="data">
                        {{ data.quantity * data.price }}
                    </template>
                </a-table>
            </a-col>
        </a-row>

        <a-row :gutter="16" type="flex" justify="space-around" align="middle" v-show="cart.length > 0">
            <a-col :span="4" ><h1 style="margin-top: 0.5em;"> Total : $ {{ total }} </h1></a-col>

            <a-col :span="4" :offset="16">
                <a-button type="primary" @click="clear"> Buy </a-button>
            </a-col>
        </a-row>

        <a-card v-show="cart.length == 0">
            <h1> Your cart don't have any goods </h1>
        </a-card>

    </div>
</template>

<script>
export default {
    name: 'Cart',
    props: {

    },
    data: function() {
        return {
            products: [
                {
                    id: 1,
                    name: 'Switch 全新主機',
                    quantity: 1,
                    price: 9970
                },
                {
                    id: 2,
                    name: 'Switch 螢光色手把',
                    quantity: 1,
                    price: 2350
                },
                {
                    id: 3,
                    name: 'Switch 充電座',
                    quantity: 1,
                    price: 1500
                },
            ],
            cart: [],
            columns: [
                {
                    title: '#',
                    align: 'left',
                    scopedSlots: { customRender: '#' }
                },
                {
                    title: 'remove',
                    align: 'left',
                    scopedSlots: { customRender: 'remove' }
                },
                {
                    title: 'good',
                    align: 'left',
                    scopedSlots: { customRender: 'good' }
                },
                {
                    title: 'quantity',
                    align: 'left',
                    scopedSlots: { customRender: 'quantity' }
                },
                {
                    title: 'price',
                    align: 'left',
                    scopedSlots: { customRender: 'price' }
                },
                {
                    title: 'total',
                    align: 'left',
                    scopedSlots: { customRender: 'total' }
                }
            ]
        } 
    },
    methods: {
        add(product) {
            if(this.cart.find(item => item.id == product.id)) {
                alert("This good already been have in cart!!!")
            } else {
                let cartItem = Object.assign({}, product)
                this.cart.push(cartItem)
            }
        },
        remove(id) {
            var index = this.getCartIndex(id)
            this.cart.splice(index, 1)
        },
        increase(id) {
            var index = this.getCartIndex(id)
            this.cart[index].quantity++
        },
        decrease(id) {
            var index = this.getCartIndex(id)
            this.cart[index].quantity <= 1 ? this.cart[index].quantity : this.cart[index].quantity--
        },
        getCartIndex(id) {
            let index = this.cart.indexOf(this.cart.find(item => item.id == id))
            return index
        },
        clear() {
            this.cart = []
            alert("Thank you for buying!!!")
        }
    },
    computed: {
        total() {
            let totalPrice = 0
            this.cart.forEach(item => totalPrice += item.quantity * item.price)
            return totalPrice
        }
    }
}
</script>