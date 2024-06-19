<template>
    <div class="banner">
        <div class="container">
            <div class="left">
                <header>
                    <img :src="logo" alt="Logo" class="logo">
                </header>
                <h1>Venha trilhar comigo a <span>Jornada do Seu Crescimento</span></h1>
                <img class="imagem-celular" :src="formBg">
                <p class="text-center">Minha história no mundo do artesanato começou em 2018, eu tive que aprender tudo
                    do zero como
                    construir um negócio de sucesso nas redes sociais. Agora quero te ensinar tudo que aprendi na minha
                    trajetória!</p>
                <div class="section-title">
                    <h2>Inscreva-se e garanta sua vaga gratuita no evento de lançamento!
                        Dia 30/06 às 18h Online e AO VIVO</h2>
                </div>
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
                            <button v-if="!isLoading"  type="submit" class="theme-btn">QUERO PARTICIPAR</button>
                            <div v-else class="loader">Enviando...</div>
                        </div>
                    </form>
                    <div v-if="successMessage" class="success-message" v-html="successMessage"></div>
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
