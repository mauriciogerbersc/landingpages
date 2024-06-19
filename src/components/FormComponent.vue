<template>
    <div class="banner">
        <div class="container">
            <div class="left">
                <header>
                    <img :src="logo" alt="Logo" class="logo">
                </header>
                <h1>Venha trilhar comigo a <span>Jornada do Seu Crescimento</span></h1>
                <img class="imagem-celular" :src="formBg">
                <p>Oi, pessoal. <strong>Eu sou a Duda da Amorino Fios</strong>, e quero convidar você para um <strong>evento muito especial</strong> que pode <strong>transformar o seu negócio de artesanato!</strong></p>
                <p>Minha história no mundo do artesanato começou em 2018. Comecei do zero, aprendendo passo a passo como construir um negócio de sucesso nas redes sociais. Foi uma jornada desafiadora, mas extremamente gratificante, e agora estou pronta para compartilhar todos os segredos e estratégias que aprendi ao longo do caminho.</p>
                <p>No dia <strong>30/06/24 às 18h</strong>, vamos nos encontrar <strong>ONLINE e AO VIVO</strong> para o lançamento do curso <strong>Artesãs Digitais: a Jornada do Seu Crescimento.</strong></p>
                <p>Este evento será uma <strong>oportunidade única</strong> para você ficar por dentro de tudo que irá acontecer, conhecer um pouco da história de pessoas muito especiais e, ainda, concorrer a uma vaga para esse curso, que poderá transformar seu Instagram em uma verdadeira vitrine de vendas, aumentar sua autoconfiança e deixar você mais próxima da liberdade financeira que sempre desejou.</p>
                <div class="section-title">
                    <h2>Inscreva-se e garanta sua vaga GRATUITA!</h2>
                </div>
                <p>Vamos juntos transformar seu negócio de artesanato e fazer de 2024 o ano da sua virada!</p>

                <p>
                    <strong>
                📅 Data: Domingo, dia 30.06 <br>
                🕕 Hora: 18h <br>
                📍 Onde: ONLINE e AO VIVO</strong>
                </p>

                <div class="lp-form">
                    <form>
                        <div class="form-group">
                            <input type="text" id="name" name="name" class="form-control" value=""
                                placeholder="Seu nome" required="">
                        </div>
                        <div class="form-group">
                            <input type="text" id="name" name="name" class="form-control" value=""
                                placeholder="Seu e-mail" required="">
                        </div>
                        <div class="form-group text-center">
                            <button v-if="!isLoading"  type="submit" class="theme-btn">[GARANTIR MINHA VAGA]</button>
                            <div v-else class="loader">Enviando...</div>
                        </div>
                    </form>
                    
                    <div v-if="successMessage" class="success-message" v-html="successMessage"></div>
                    <p>Estou muito animada para compartilhar tudo sobre essa jornada! Até lá! 💖</p>
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
            phone: '',
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
                    phone: this.phone,
                });

                this.successMessage = "Seu interesse foi registrado com sucesso!";
                
                this.name = '';
                this.email = '';
                this.phone = '';
            } catch (error) {
                console.error('Erro ao cadastrar usuário:', error);
            } finally {
                this.isLoading = false;
            }
        }
    }
}
</script>

<style scoped>
.success-message {
  margin-top: 20px;
  padding: 10px;
  background-color: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
  border-radius: 5px;
}
</style>
