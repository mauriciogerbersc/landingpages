<template>
    <div class="banner">
        <div class="container">
            <div class="left">
                <header>
                    <img :src="logo" alt="Logo" class="logo">
                </header>
                <h1>Venha trilhar comigo a <span>Jornada do Seu Crescimento</span></h1>
                <img class="imagem-celular" :src="formBg">
                <p>Minha história no mundo do artesanato começou em 2018. Comecei do zero, aprendendo passo a passo <strong>como construir um negócio de sucesso</strong> nas redes sociais. Foi uma jornada desafiadora, mas extremamente gratificante, e agora estou pronta para <strong>compartilhar todos os segredos e estratégias</strong> que aprendi ao longo do caminho.</p>
                <p style="margin-bottom: 0;">Este evento será uma <strong>oportunidade única para você</strong> ficar por dentro de tudo que irá acontecer, conhecer um pouco da <strong>história de pessoas muito especiais</strong> e, ainda, <strong>concorrer a uma vaga para</strong> esse curso, que poderá <strong>transformar seu Instagram</strong> em uma verdadeira vitrine de vendas, <strong>aumentar sua autoconfiança</strong> e deixar você mais próxima da <strong>liberdade financeira</strong> que sempre desejou.</p>
                
                <div class="section-title">
                    <h2>Inscreva-se e garanta sua vaga GRATUITA!</h2>
                </div>
                <p>Vamos juntas transformar seu negócio de artesanato e fazer de 2024 o ano da sua virada!</p>

                <p>
                    <strong>
                    📅 Data: Domingo, dia 30.06 <br>
                    🕕 Hora: 18h <br>
                    📍 Onde: ONLINE e AO VIVO
                    </strong>
                </p>

                <p>Se inscreva no formulário abaixo:</p>
                <div class="lp-form">
                    <form @submit.prevent="submitForm">
                        <div class="form-group">
                            <input type="text" v-model="name" id="name" name="name" class="form-control" value=""
                                placeholder="Seu nome" required="">
                        </div>
                        <div class="form-group">
                            <input type="text" v-model="email" id="email" name="email" class="form-control" value=""
                                placeholder="Seu e-mail" required="">
                        </div>
                        <div class="form-group text-center">
                            <button v-if="!isLoading"  type="submit" class="theme-btn">GARANTIR MINHA VAGA</button>
                            <div v-else class="loader"></div>
                        </div>
                    </form>
                    
                    <div v-if="successMessage" class="success-message" v-html="successMessage"></div>
                    <div v-if="errorMessage" class="error-message" v-html="errorMessage"></div>
                    <p> Estou muito animada para compartilhar tudo sobre essa jornada! Até lá! 💖</p>
                </div>
            </div>
            <div class="right">
                <img :src="formBg">
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            name: '',
            email: '',
            successMessage: '',
            isLoading: false,
            formBg: require('@/assets/images/form-bg.png'),
            backgroundImage: require('@/assets/images/lp-two.png'),
            logo: require('@/assets/images/AD_horizontal 4.png'),
        };
    },
    computed: {
        backgroundImageStyle() {
            return {
                'background-image': `url(${this.backgroundImage})`
            };
        }
    },
    methods: {
        async submitForm() {
            this.isLoading = true;
            try {
                await axios.post('http://localhost/api/lead', {
                    name: this.name,
                    email: this.email,
                });

                this.successMessage = "Seu interesse foi registrado com sucesso!";
                
                this.errorMessage = '';
                this.name = '';
                this.email = '';
            } catch (error) {
                this.successMessage = '';
                if (error.response && error.response.data) {
                    this.errorMessage = error.response.data.message || 'Error submitting form';
                } else {
                    this.errorMessage = 'Error submitting form';
                }
            } finally {
                this.isLoading = false;
            }
        }
    }
}
</script>

<style scoped>
.success-message {
  margin: 20px;
  padding: 10px;
  background-color: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
  border-radius: 5px;
}
.error-message {
  margin: 20px;
  padding: 10px;
  background-color: #ff0000;
  color: #c7a1a1;
  border: 1px solid #c3e6cb;
  border-radius: 5px;
}
</style>
