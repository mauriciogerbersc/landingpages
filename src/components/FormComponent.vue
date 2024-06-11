<template>
   <body class="lp">
    <div class="page-wrapper">
        <section class="one-page bgp-bottom bgp-bottom bgc-black py-50 rpt-95 rpb-100" :style="backgroundImageStyle">
            <div class="container">
                <div class="row gap-150 justify-content-center">
                    <div class="lp-content style-two text-white">
                        <h1>Venha trilhar comigo a jornada do <span>seu crescimento</span></h1>
                    </div>

                    <div class="col-lg-6 ">
                        <div class="lp-form-bg">
                            <img :src="formBg">
                        </div>
                    </div>
           
                    <div class="col-lg-6 rel z-1">
                        <div class="lp-content style-two text-white">
                            <p>
                                Minha história no mundo do artesanato começou em 2018, eu tive que aprender tudo do zero, desde as técnicas de artesanato até a construção de um negócio de sucesso nas redes sociais. 
                            </p>
                            <p>Consegui me destacar nesse mercado e criar duas empresas do ramo, alcançando todos os estados brasileiros e mais de 30 países.</p>
                            <p>Agora vou ajudar você a construir um caminho de sucesso. Se você quer transformar sua paixão pelo artesanato em um negócio próspero, eu te convido a participar do nosso evento de lançamento gratuito!</p>
                  
                            <div class="lp-content style-two text-white">
                                <h4><span>Garanta seu lugar no evento de lançamento gratuito:</span></h4>
                            </div>

                            <div class="lp-form">

                                <form @submit.prevent="submitForm">
                                    <div class="form-group">
                                        <input type="text" id="name" v-model="name" required class="form-control" value=""
                                            placeholder="Seu nome">
                                    </div>
                                    <div class="form-group">
                                        <input type="text" id="name" v-model="email" class="form-control" value=""
                                            placeholder="Seu e-mail" required>
                                    </div>
                                    <div class="form-group">
                                        <input type="text" id="name" v-model="phone" class="form-control" value=""
                                            placeholder="Seu whatsapp" required>
                                    </div>
                                    <div class="form-group py-30 mb-0">
                                        <button v-if="!isLoading" type="submit" class="theme-btn">QUERO PARTICIPAR <i class="fas fa-solid fa-arrow-right"></i></button>
                                        <div v-else class="loader">Enviando...</div>
                                    </div>
                                </form>
                                <div v-if="successMessage" class="success-message" v-html="successMessage"></div>
                            </div>

                        </div>
                    </div>
                </div>
            
              </div>
        </section>

        <footer class="main-footer">
            <div class="container">
                <div class="footer-bottom">
                    <div class="row align-items-center">
                        <div class="col-xl-12 col-lg-12">
                            <div class="copyright-text pt-10 text-lg-start text-center">
                                <p style="color:grey">Copyright 2024. Todos os direitos reservados</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </footer>

    </div>
</body>
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
            formBg: require('@/assets/images/IMG_6169.png'),
            backgroundImage: require('@/assets/images/lp-two.png'),
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
