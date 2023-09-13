<template>
    <section class="main-container">
        <ul class="left-col" ref="navBtns" @click="sectionSwitch">
            <li class="nav-btn active" data-id="1">
                <div class="num" >1</div>
                <div class="title" >
                    <h3 class="child" >step 1</h3>
                    <p class="child" >your info</p>
                </div>
            </li>
            <li class="nav-btn" data-id="2">
                <div class="num">2</div>
                <div class="title"> 
                    <h3 class="child">step 2</h3>
                    <p class="child">select plans</p>
                </div>
            </li>
            <li class="nav-btn" data-id="3">
                <div class="num">3</div>
                <div class="title">
                    <h3 class="child">step 3</h3>
                    <p class="child">add-ons</p>
                </div>
            </li>
            <li class="nav-btn" data-id="4">
                <div class="num">4</div>
                <div class="title">
                    <h3 class="child">step 4</h3>
                    <p class="child">summary</p>
                </div>
            </li>
        </ul>
        <div class="right-col">
            <div class="content">
                <div class="top-section" ref="sectionLists">
                    <div class="top-row active" data-id="info" data-num="1">
                        <div class="form-head">
                            <h1>Personal info</h1>
                            <p>Please provide your name, email address, and phone number.</p>
                        </div>
                        <div class="inputs">
                            <article class="inpit-field">
                                <div class="label-cont">
                                    <label for="name">name</label>
                                    <label for="error" class="error">This field is required</label>
                                </div>
                                <input type="text" id="name" placeholder="e.g Stephen King" v-model="name" ref="names">
                            </article>
                            <article class="inpit-field">
                                <div class="label-cont">
                                    <label for="email">email</label>
                                    <label for="error" class="error">This field is required</label>
                                </div>
                                <input type="email" id="email" placeholder="e.g stephenking@lorem.com" v-model="mail" ref="email">
                            </article>
                            <article class="inpit-field">
                                <div class="label-cont">
                                    <label for="phone">phone number</label>
                                    <label for="error" class="error">This field is required</label>
                                </div>
                                <input type="number" id="phone" placeholder="e.g +1 234 567 890" v-model="phone" ref="phoneNum">
                            </article>
                        </div>
                    </div>

                    <div class="top-row plan" data-id="plan" data-num="2">
                        <div class="form-head">
                            <h1>Select your plan</h1>
                            <p>You have the option of monthly or yearly billing.</p>
                        </div>
                        <div class="inputs plans" ref="cards">
                            <article class="card" v-for="plan in plans" :key="plan.id" @click="selectPlan" :data-id="plan.id">
                                <img :src="require(`@/assets/images/${plan.src}`)" alt="" class="">
                                <div class="info">
                                    <div>
                                        <h3>{{ plan.title }}</h3>
                                        <p>$<span ref="price" :class="{ monthPrice: !yearToggled}">{{ plan.price }}</span>/<span ref="period">month</span></p>
                                    </div>
                                    <h4 v-if="yearToggled">2 months free</h4>
                                </div>
                            </article>
                        </div>
                        <div class="period-toggle" :class="{ year: yearToggled }">
                            <h3 class="month" :class="{ active: !yearToggled}">monthly</h3>
                            <div class="toggle" @click="planToggle"><span></span></div>
                            <h3 class="year" :class="{ active: yearToggled }">yearly</h3>
                        </div>
                    </div>

                    <div class="top-row add" data-id="add" data-num="3">
                        <div class="form-head">
                            <h1>Pick add-ons</h1>
                            <p>Add-ons help enhance your gaming experience.</p>
                        </div>
                        <div class="inputs add-ons" ref="add">
                           <article class="option card" @click="selectAdd" v-for="item in addOns" :key="item.id" :data-id="item.id">
                                <input type="checkbox">
                                <div class="label">
                                    <h3>{{ item.title }}</h3>
                                    <p>{{ item.descr }}</p>
                                </div>
                                <h3 class="sub">+$<span class="numb">{{ item.price }}</span>/<span class="mnth">mo</span></h3>
                           </article>
                           
                        </div>
                    </div>

                    <div class="top-row summary" data-id="summary" data-num="4">
                        <div class="form-head">
                            <h1>Finishing up</h1>
                            <p>Double-check if everything looks OK before confirming.</p>
                        </div>
                        <div class="inputs" :class="{ toYear: yearToggled}">
                            <div class="container">
                                <article class="plan-summ">
                                    <div class="col1">
                                        <h3>{{ planTitle }} (<span ref="period3">month</span>ly)</h3>
                                        <a href="#" @click="handleChange">change</a>
                                    </div>
                                    <h3>$
                                    <span v-if="!yearToggled">{{ planPrice }}</span>
                                    <span v-else>{{ planPrice * 10 }}</span>
                                    /<span class="mnth">mo</span></h3>
                                </article>
                                <article class="add-summ">
                                    <div class="add-option" v-for="item in addOnArray" :key="item.id">
                                        <h3>{{ item.title }}</h3>
                                        <p>+$
                                            <span v-if="!yearToggled">{{ item.price }}</span>
                                            <span v-else>{{ item.price * 10 }}</span>/
                                            <span v-if="!yearToggled">mo</span>
                                            <span v-else>yr</span>
                                            
                                        </p>
                                    </div>
                                </article>
                            </div>
                            <div class="row2 add-option">
                                <h3>Total (per <span ref="period2">month</span>)</h3>
                                <p>+${{ totalPrice }}/<span class="mnth">mo</span></p>
                            </div>
                        </div>
                    </div>

                    <div class="top-row close" data-id="close" data-num="5">
                        <div>
                            <img src="../assets/images/icon-thank-you.svg" alt="thank you">
                            <h3>Thank you!</h3>
                            <p>Thanks for confirming your subscription! Wehope you have fun using our platform. If you ever need support feel free to email us at support@loremgaming.com.</p>
                        </div>
                    </div>
                </div>

                <div class="btm-row btns" @click="btnSwitch" v-if="showBtm">
                    <button class="back-btn" :class="{ showBtn: back}">go back</button>
                    <div class="ctrl-btns">
                        <button class="next-btn" v-if="next" @click="handleNext">next step</button>
                        <button class="confirm-btn" v-else @click="confirmForm">confirm</button>
                    </div>
                </div>
            </div>
        </div>
    </section>

</template>

<script>
import { computed, ref } from 'vue';

    export default {
        setup(){
            const navBtns = ref(null)
            const sectionLists = ref(null)
            const targetId = ref(1)
            const next = ref(true)
            const back = ref(false)
            const curNum = ref(1)
            const yearToggled = ref(false)
            const price = ref(null)
            const period = ref(null)
            const cards = ref(null)
            const add = ref(null)
            const period2 = ref(null)
            const period3 = ref(null)
            const showBtm = ref(true)
            const per = ref([])
            const planPrice = ref('')
            const planTitle = ref('')
            let addOnArray = ref([])
            let newObj

            const phone = ref('')
            const phoneNum = ref(null)
            const name = ref('')
            const names = ref(null)
            const mail = ref('')
            const email = ref(null)

            const plans = [
                {
                    id: 1,
                    src: 'icon-arcade.svg',
                    title: 'arcade',
                    price: 9,

                },
                {
                    id: 2,
                    src: 'icon-advanced.svg',
                    title: 'advanced',
                    price: 12,

                },
                {
                    id: 3,
                    src: 'icon-pro.svg',
                    title: 'pro',
                    price: 15,

                },
            ]

            const addOns = [
                {
                    id: 1,
                    title: 'Online service',
                    price: 1,
                    descr: 'Access to multiplayer game'
                },
                {
                    id: 2,
                    title: 'Larger storage',
                    price: 2,
                    descr: 'Extra 1TB of cloud save'
                },
                {
                    id: 3,
                    title: 'Customizeable profile',
                    price: 2,
                    descr: 'Custom theme on your profile'
                }

            ]

            const totalPrice = computed(()=>{
                let num = ref(0)
                addOnArray.value.forEach(item=>{
                    num.value += item.price
                })

                let total = num.value + Number(planPrice.value)
                 if(yearToggled.value){
                        total = total * 10
                        
                    } else {
                        total = total
                    }
                return total
            })

           
                      

            
            function selectAdd(e){
                const addList = [...add.value.children]
                const targetElement = e.currentTarget
                const targetID = targetElement.dataset.id
                
                targetElement.children[0].checked = !targetElement.children[0].checked
                addList.forEach(item=>{
                    if(item.children[0].checked){
                        item.classList.add('active')
                       
                    } else {
                        item.classList.remove('active')
                    }
                })


                if(targetElement.children[0].checked){
                    addOns.forEach(item=>{
                        if(item.id == targetID){
                            newObj = {
                                title: item.title,
                                price: item.price,
                                id: item.id
                            }
                        }
                    })
                    addOnArray.value.push(newObj)
                } else {
                    addOnArray.value = addOnArray.value.filter(item=> item.id != targetID)
                }
    
            }

            function planToggle(){
                yearToggled.value = !yearToggled.value

                const planPeriod = [...period.value]
                const planPrice = [...price.value]
                planPeriod.forEach((item)=>{
                    if(item.innerText === 'month'){
                        item.innerText = 'year'
                    } else {
                        item.innerText = 'month'
                    }
                })

                const addCost = [...document.querySelectorAll('.numb')]
                const addPeriod = [...document.querySelectorAll('.mnth')]

                
                addCost.forEach(item=>{
                    if(!yearToggled.value){
                        const num = Number(item.innerText) / 10
                        item.innerText = num
                    } else {
                        const num = Number(item.innerText) * 10
                        item.innerText = num
                    }
                })

                addPeriod.forEach(item=>{
                    if(!yearToggled.value){
                        item.innerText = 'mo'
                    } else {
                        item.innerText = 'yr'
                    }
                })

                planPrice.forEach(item=>{
                    if(!yearToggled.value){
                        const num = Number(item.innerText) / 10
                        item.innerText = num
                    } else {
                        const num = Number(item.innerText) * 10
                        item.innerText = num
                    } 
                })

                if(yearToggled.value){
                    period2.value.innerText = 'year'
                    period3.value.innerText = 'year'
                } else {
                    period2.value.innerText = 'month'
                    period3.value.innerText = 'month'
                }
            }

             function selectPlan(e){
                const targetElement = e.currentTarget
                const targetID = targetElement.dataset.id
                const cardList = [...cards.value.children]
                cardList.forEach(card=>{
                    if(card.classList.contains('active')){
                        card.classList.remove('active')
                    }
                })

                plans.forEach(item=>{
                    if(item.id == targetID){
                        planPrice.value = item.price
                        planTitle.value = item.title
                    }
                })

                targetElement.classList.add('active')
            }
            

            function sectionSwitch(e){
                const targetElement = e.target
                const parentTarget = targetElement.parentElement
                const grandTarget = parentTarget.parentElement
                const list = [...sectionLists.value.children]
                const btnsList = [...navBtns.value.children]
                

                if(targetElement.classList.contains('nav-btn') || parentTarget.classList.contains('nav-btn') || grandTarget.classList.contains('nav-btn')){
                    btnsList.forEach(btn=>{
                        btn.classList.remove('active')
                    })

                    if(targetElement.classList.contains('title') || targetElement.classList.contains('num')){
                        targetId.value = parentTarget.dataset.id
                        parentTarget.classList.add('active')
                    }

                    if(targetElement.classList.contains('child')){
                        targetId.value = grandTarget.dataset.id
                        grandTarget.classList.add('active')
                    }

                    btnToggle(targetId)

                    list.forEach(item=>{
                        item.classList.remove('active')

                        if(item.dataset.num === targetId.value){
                            curNum.value = item.dataset.num
                            item.classList.add('active')
                        }
                    })
                }  
               
            }

            function btnToggle2(num){
                if(num > 0){
                    back.value = true
                }

                if(num == 1){
                    back.value = false
                }

                if(num > 3){
                    next.value = false
                } else {
                    next.value = true
                }
            }

            function pageChange(pageNum) {
                const list = [...sectionLists.value.children]
                const btnsList = [...navBtns.value.children]
                const num = ref(null)
                num.value = pageNum
                list.forEach(item=>{
                    item.classList.remove('active')

                     if(item.dataset.num == num.value){
                            item.classList.add('active')
                        }
                })

                btnsList.forEach(item=>{
                    item.classList.remove('active')
                })
                
                listSwitch(list, btnsList, num.value) 
                btnToggle2(num.value)
            }

            function handleChange(){
                pageChange(2)
            }

             function btnSwitch(e){
                    const targetElement = e.target
                    const list = [...sectionLists.value.children]
                    const btnsList = [...navBtns.value.children]
                    const num = ref(1)
                    const fields = [phoneNum.value, names.value, email.value]
                    let page

                    list.forEach(item=>{
                        if(item.classList.contains('active')){
                            page = item
                            num.value = item.dataset.num

                        }
                        item.classList.remove('active')
                    })

                     btnsList.forEach(btn=>{
                        btn.classList.remove('active')
                    })

                    function inputValidation(field, input){
                        if(!input.value){
                            page.classList.add('active')
                            pageChange(1)
                            field.value.parentElement.classList.add('errorField')
                        } else {
                            field.value.parentElement.classList.remove('errorField')
                        }
                    }

                    if(targetElement.classList.contains('back-btn')){
                        num.value--
                        console.log(num.value)
                        listSwitch(list, btnsList, num.value)
                    }

                    if(targetElement.classList.contains('next-btn')){
                        const list = [...sectionLists.value.children]

                        if(page.dataset.num == 1 && (!phone.value || !name.value.length || !mail.value.length)) {
                            inputValidation(phoneNum, phone, page)
                            inputValidation(names, name, page)
                            inputValidation(email, mail, page)
                            console.log(phone.value.length)
                        } else {
                            fields.forEach(item=>{
                                item.parentElement.classList.remove('errorField')
                            })
                            num.value++
                            console.log(num.value)
                            listSwitch(list, btnsList, num.value)
                            btnToggle2(num.value)
                        }

                        if(page.dataset.num == 2 && !planTitle.value.length){
                            alert('select plan')
                            pageChange(2)
                        } else {
                            
                        } 
                    }

                    if(targetElement.classList.contains('confirm-btn')){
                        if(!phone.value || !name.value.length || !mail.value.length){
                            alert('Enter User Details')
                            pageChange(1)
                        } else {
                            num.value++
                            listSwitch(list, btnsList, num.value)
                            showBtm.value = false
                        }
                    }
                    
                }

                function btnToggle(targetId){
                    showBtm.value = true
                    if(targetId.value > 0){
                        back.value = true
                    }

                    if(targetId.value == 1){
                        back.value = false
                    }

                    if(targetId.value > 3){
                        next.value = false
                    } else {
                        next.value = true
                    }
                }

                function listSwitch(list, btnsList, num){
                    list.forEach(item=>{
                        
                        if(item.dataset.num == num){
                            
                            item.classList.add('active')
                        }
                    })

                    btnsList.forEach(btn=>{
                        if(btn.dataset.id == num){
                            btn.classList.add('active')
                        }
                    })
                    btnToggle(num)
                }


            return { navBtns, sectionLists, sectionSwitch, next, back, btnSwitch, plans, yearToggled, planToggle, period, price, cards, selectPlan, selectAdd, add, period2, period3, per, showBtm, phone, phoneNum, mail, email, name, names, addOns, planPrice, planTitle, addOnArray, totalPrice, handleChange }
        }
        
    }
</script>

<style scoped>
    .main-container {
        width: 70vw;
        padding: 1rem;
        border-radius: 1rem;
        display: grid;
        grid-template-columns: 30% 70%;
        background: var(--White);
    }
    .left-col {
        background: url("../assets/images/bg-sidebar-desktop.svg");
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
        padding: 2rem;
        border-radius: 1rem;
        height: 80vh;
    }

    .nav-btn {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        margin-bottom: 1.5rem;
        cursor: pointer;
    }

    .num, .nav-btn h3, .nav-btn p {
        font-weight: 700;
        font-size: 0.8rem;
    }

    .nav-btn .num {
        height: 2rem;
        width: 2rem;
        border: 1.5px solid var(--Magnolia);
        border-radius: 50%;
        display: grid;
        place-items: center;
        color: var(--Magnolia);
        align-self: center;
        transition: var(--transition);
    }

    .nav-btn:hover .num {
        background: var(--Magnolia);
        color: var(--Marine-blue);
    }

    .active .num {
        background: var(--Magnolia);
        color: var(--Marine-blue);
    }

    .nav-btn h3 {
        text-transform: uppercase;
        font-size: 0.78rem;
        color: var(--Cool-gray);
        margin-bottom: 0.1rem;
    }

    .nav-btn p {
        text-transform: uppercase;
        color: var(--Magnolia);
        letter-spacing: 1px;
    }

    .right-col {
        width: 100%;
        height: 100%;
        padding-top: 1rem;
    }

    .right-col .content {
        width: 70%;
        height: 100%;
        margin: 0 auto;
        display: grid;
        grid-template-rows: 1fr auto;
    }

    .form-head {
        margin-bottom: 2rem;
    }

    .form-head h1 {
        font-weight: 700;
        font-size: 2rem;
        margin-bottom: 0.35rem;
        color: var(--Marine-blue);
    }

    .form-head p {
        color: var(--Cool-gray);
        font-size: 1rem;
    }

    label {
        text-transform: capitalize;
        color: var(--Marine-blue);
        font-weight: 500;
    }

    input {
        display: block;
        margin: 0.5rem 0 1.3rem;
        width: 100%;
        padding: 0.85rem;
        border: 1px solid var(--Cool-gray);
        border-radius: 0.5rem;
        color: var(--Marine-blue);
        font-weight: 700;
        transition: var(--transition);
    }

    input::-webkit-inner-spin-button, input::-webkit-outer-spin-button{
        -webkit-appearance: none;
        margin: 0;
    }
    
    input[type=number]{
        -moz-appearance: textfield;
    }

    .label-cont {
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .error {
        color: var(--Strawberry-red);
        font-weight: 700;
        font-size: 0.7rem;
        opacity: 0;
        z-index: -1;
        transition: var(--transition);
    }

    .errorField .error{
        opacity: 1;
        z-index: 1;
    }

    .errorField {
        border-color: var(--Strawberry-red);
    }

    input:hover, input:focus {
        border-color: var(--Purplish-blue);
        outline: none;
    }

    .btns {
        display: flex;
        align-items: center;
        justify-content: space-between;
        
    }

    .btns button {
        background: var(--Marine-blue);
        color:var(--Magnolia) ;
        text-transform: capitalize;
        border: 1px solid transparent;
        padding: 0.7rem 1.5rem;
        border-radius: 0.3rem;
        cursor: pointer;
        transition: var(--transition);
        font-weight: 500;
        letter-spacing: 1px;
    }

    .btns .back-btn {
        background: transparent;
        color: var(--Cool-gray);
        font-weight: 700;
        padding: 0.7rem 0;
        opacity: 0;
        z-index: -1;
    }

    .back-btn.showBtn {
        opacity: 1;
        z-index: 1;
    }

    .btns .back-btn:hover {
        color: var(--Marine-blue);
    }

    .btns .confirm-btn {
        background: var(--Purplish-blue);
    }

    .btns .confirm-btn:hover, .next-btn:hover {
        opacity: 0.7;
    }

    .top-section {
        position: relative;
        width: 100%;
    }

    .top-row {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        opacity: 0;
        z-index: -1;
        transition: all 0.3s linear;
    }

    .top-row.active, .close.active {
        z-index: 1;
        opacity: 1;
    }

    

    .card {
        border: 1px solid var(--Light-gray);
        border-radius: 0.5rem;
        padding: 1rem;
        transition: var(--transition);
        cursor: pointer;
    }

    .card.active {
        background: var(--Alabaster);
        border-color: var(--Purplish-blue);
    }

    .card:hover {
        background: var(--Alabaster);
        border-color: var(--Purplish-blue);
    }

    .card img {
        margin-bottom: 3.5rem;
    }

    .info :is(h3, p, h4){
        font-weight: 500;
        font-size: 0.8rem;
        margin-bottom: 0.3rem;
    }

    .info h3 {
        color: var(--Marine-blue);
        font-weight: 700;
        font-size: 1rem;
        text-transform: capitalize;
    }

    .info p {
        color: var(--Cool-gray);
       font-weight: 0;
    }

    .info h4 {
        color: var(--Marine-blue);
        
    }

    .plans {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 1rem;
        width: 100%;
    }

    .period-toggle {
        width: 100%;
        background: var(--Alabaster);
        border-radius: 0.5rem;
        margin-top: 1.5rem;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 1rem;
        gap: 1rem;
    }

    .period-toggle h3 {
        font-size: 0.8rem;
        text-transform: capitalize;
        color: var(--Cool-gray);
        cursor: pointer;
        transition: var(--transition);
    }

    .period-toggle h3:hover {
        color: var(--Marine-blue);
    }

    .period-toggle .active {
        color: var(--Marine-blue);
    }

    .toggle {
        width: 3.5rem;
        height: 1.5rem;
        background: var(--Marine-blue);
        border-radius: 1rem;
        display: flex;
        align-items: center;
        justify-content: start;
        padding: 0.3rem;
        cursor: pointer;
        transition: var(--transition);
    }

    .year .toggle {
         justify-content: end;
    }

    .toggle span {
        height: 100%;
        width: 30%;
        background: white;
        border-radius: 50%;
    }

    .option {
        display: grid;
        align-items: center;
        grid-template-columns: auto 1fr auto;
        gap: 1rem;
        margin-bottom: 1rem;
    }

    .option input[type="checkbox"] {
        width: 1rem;
        height: 1rem;
        margin: auto 0;
    }

    .label h3 {
        font-size: 1rem;
        color: var(--Marine-blue);
    }

    .label p {
        font-size: 0.85rem;
        font-weight: 500;
        color: var(--Cool-gray);
        margin-top: 0.3rem;
    }

    .option .sub {
        font-size: 0.9rem;
        color: var(--Purplish-blue);
    }

    .container {
        background: var(--Alabaster);
        border-radius: 1rem;
        margin-bottom: 1rem;
        padding: 1rem;
    }

    .container article {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding-bottom: 1rem;
        border-bottom: 1px solid var(--Light-gray);
    }

    .container article:last-of-type {
        border: none;
        padding: 1rem 0 0;
    }

    .add-summ {
        display: flex;
        flex-direction: column;
        gap: 1rem;
       
    }

    .add-option {
        display: flex;
        align-items: center;
        justify-content: space-between;
        width: 100%;
    }

    .plan-summ h3 {
        color: var(--Marine-blue);
        font-size: 1rem;
        text-transform: capitalize;
    }

    .col1 h3 {
        margin-bottom: 0.3rem;
    }

    .col1 a {
        color: var(--Cool-gray);
        text-transform: capitalize;
        transition: var(--transition);
        cursor: pointer;
    }

    .col1 a:hover {
        color: var(--Purplish-blue);
    }

    .add-option h3 {
        color: var(--Cool-gray);
        font-weight: 500;
        font-size: 0.95rem;
        
    }

    .add-option p {
        color: var(--Marine-blue);
        font-size: 0.9rem;
        font-weight: 500;
    }

    .row2 {
        padding: 0 1.5rem;
    }

    .close {
        display: grid;
        place-items: center;
        text-align: center;
        height: 100%;
    }

    .close img {
        margin-bottom: 1rem;
    }

    .close h3 {
        margin-bottom: 0.8rem;
        font-size: 2rem;
        font-weight: 700;
        color: var(--Marine-blue);
    }

    .close p {
        font-weight: 500;
        color: var(--Cool-gray);
        line-height: 1.5;
    }

    @media only screen and (max-width: 1000px){
        .main-container {
            grid-template-columns: 1fr;
            height: 40rem;
            grid-template-rows: auto 1fr;
            padding: 0;
            background: var(--Magnolia);
            border-radius: 0;
            position: relative;
        }

        .left-col {
            height: auto;
            display: flex;
            justify-content: center;
            gap: 1rem;
            background: url('../assets/images/bg-sidebar-mobile.svg');
            background-position: center;
            background-repeat: no-repeat;
            background-size: cover;
            border-radius: 0;
            padding-bottom: 4rem;
        }

        .nav-btn .title {
            display: none;
        }

        .top-section {
            position: unset;
            width: 100%;
        }

        .right-col .top-row {
            padding: 1.5rem 1rem;
            width: 90%;
            height: auto;
            left: 50%;
            top: 6rem;
            transform: translateX(-50%);
            background: var(--White);
            border-radius: 0.5rem;
        }

        .right-col .content {
            width: 100%;
        }

        .btns {
            width: 100%;
            position: relative;
            background: var(--White);
            padding: 0.5rem 1rem;
        }

        .plans {
            grid-template-columns: 1fr;
            gap: 0.5rem;
        }

        .plans .card {
            display: flex;
            gap: 1rem;
            padding: 0.8rem;
        }

        .card img {
            margin: 0;
        }

        .form-head p {
            font-size: 0.8rem;
        }

        .info h3 {
            font-size: 0.9rem;
        }

        .info {
            flex: 1;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

         .top-row.close {
            padding: 4rem 2rem;
        }

        .top-row.close img {
            width: 3rem;
        }
    }

    @media only screen and (max-width: 600px){

        
        .main-container {
            width: 100%;
        }
    }


</style>