<template>
  <v-app> 
    <!--
    <v-toolbar
      src="https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg"
    >
      <v-spacer></v-spacer>
      <v-card-title class="white--text mt-1">
        <v-sheet elevation="5">
          <v-avatar tile size="60">
            <img
              alt="user"
              src="https://images.multipedidos.com.br/profiles/21a09d8243a2d0512c77135e2eb74c4ae084b4cc21b4a32af076ed4a676c4edf.jpg"
            >
          </v-avatar>
        </v-sheet>  
        <p class="ml-3">
          Vizinho's Hamburgueria
        </p>        
      </v-card-title>
      <v-spacer></v-spacer>
    </v-toolbar>
    -->
    <v-card flat>
      <v-toolbar
        src="https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg"
        extended
        flat
        style="min-height: 150px;"
      >
        <!--<v-app-bar-nav-icon></v-app-bar-nav-icon>-->
      </v-toolbar>
      
      <v-card
        class="mx-auto"
        max-width="700"
        style="margin-top: -64px;"
      >
        <v-toolbar flat>
          <v-spacer></v-spacer>         
          <v-toolbar-title class="black--text">
            <v-card-text width="100" style="margin-top: -20px;">
              <v-sheet elevation="5" width="100">
                <v-avatar tile size="100" width="100">
                  <img
                    alt="Vizinho's"
                    src="https://images.multipedidos.com.br/profiles/21a09d8243a2d0512c77135e2eb74c4ae084b4cc21b4a32af076ed4a676c4edf.jpg"
                  >
                </v-avatar>
              </v-sheet>
            </v-card-text>
          </v-toolbar-title>
          <v-spacer></v-spacer>
        </v-toolbar>
        <v-toolbar flat>
          <v-spacer></v-spacer>         
          <v-toolbar-title class="black--text text-center">
            Vizinho's Hamburgueria<br>
            <span class="caption primary--text" @click="linkexterno('https://goo.gl/maps/AfJTjRXbUFogsbFb9')">Rua aritiba, 680 - Realengo, Rio de janeiro</span>
          </v-toolbar-title>
          <v-spacer></v-spacer>
        </v-toolbar>
        <v-divider></v-divider>
        <v-card-text>
          <v-list class="transparent">
            <v-list-item>
              <v-list-item-subtitle class="text-center">Entregas<br> 20-30 min</v-list-item-subtitle>
              <v-list-item-subtitle class="text-center">
                Funcionamento<br>
                Ter. a Dom.
                <br> 17h às 01h
                <br>
                <v-icon>
                  mdi-clock-outline
                </v-icon>
                
              </v-list-item-subtitle>
              
              <v-list-item-subtitle class="text-center">
                Retiradas<br> 10-20 min
              </v-list-item-subtitle>
            </v-list-item>
            <v-list-item>
              <v-list-item-subtitle class="text-center">
                Pix
                <br>
                <v-icon>
                  mdi-rhombus-split
                </v-icon>
              </v-list-item-subtitle>
              <v-list-item-subtitle class="text-center">
               Cartão
                <br>
                <v-icon>
                  mdi-credit-card-outline
                </v-icon>
              </v-list-item-subtitle>
              <v-list-item-subtitle class="text-center">
                Dinheiro
                <br>
                <v-icon>
                  mdi-cash
                </v-icon>
              </v-list-item-subtitle>
            </v-list-item>
          </v-list>
        </v-card-text>
        <v-tabs
          v-model="tab"
          fixed-tabs
          color="red"
        >
          <v-tab
            v-for="tabitem in tabs"
            :key="tabitem.title"
          >
            {{ tabitem.title }}
          </v-tab>
        </v-tabs>
        <v-row >
          <!--
          <v-fab-transition>           
            <v-btn
              v-show="!dialog"
              @click="dialog=true"
              color="error"
              dark
              absolute
              bottom
              right
              fab
            >
              <v-badge
                :content="1"
                color="error"
              >
                <v-icon>mdi-cart</v-icon>
              </v-badge>
            </v-btn>          
          </v-fab-transition>
          -->
          <v-col>
            <!--
            <v-card class="logo py-4 d-flex justify-center">
              <NuxtLogo />
              <VuetifyLogo />
            </v-card>
            -->
            <v-tabs-items v-model="tab">
              <v-tab-item
                v-for="tabsitem in tabs"
                :key="tabsitem.title"
              >
                <v-card>
                  <p class="title text-center">
                    <v-alert
                      dense
                      border="bottom"
                      colored-border
                      color="red"
                    >
                    {{tabsitem.title}}
                    </v-alert>
                  </p>
                  <v-list
                    elevation="3"
                  >
                    <!--<v-subheader>{{tabsitem.title}}</v-subheader>-->
                    <v-list-item three-line v-for="subitens in tabsitem.itens" :key="subitens.title">
                      <v-list-item-avatar tile size="80">
                        <v-img
                          :alt="subitens.titulo"
                          :src="subitens.src"
                        ></v-img>
                      </v-list-item-avatar>
                      <v-list-item-content @click="dialog=true, productpage=subitens, adicionacarrinho(subitens)">
                        <v-list-item-title>{{subitens.titulo}}</v-list-item-title>
                        <v-list-item-subtitle>{{subitens.descricao}}</v-list-item-subtitle>
                        <v-list-item-subtitle class="text-subtitle-2 red--text">R$ {{real(subitens.valor)}}</v-list-item-subtitle>
                      </v-list-item-content>                  
                    </v-list-item>
                    <v-divider inset></v-divider>
                  </v-list>                                        
                </v-card>
              </v-tab-item>
            </v-tabs-items>
            <v-dialog
              v-model="dialog"
              fullscreen
              hide-overlay
              transition="dialog-bottom-transition"
            >
              <v-card tile>
                <v-toolbar
                  dark
                  color="red"
                >
                  <v-btn
                    icon
                    dark
                    @click="dialog = false"
                  >
                    <v-icon>mdi-chevron-left</v-icon>
                  </v-btn>
                  <v-toolbar-title>Produtos escolhidos ({{objetocarrinho.length}})</v-toolbar-title>                  
                </v-toolbar>
                <v-card-text>
                  <v-list
                    three-line
                    subheader
                  > 
                    <!--<v-subheader>Produtos escolhidos ({{objetocarrinho.length}})</v-subheader>-->
                    <v-list-item three-line v-for="product in exibecarrinho()" :key="product.id">
                      <v-list-item-avatar size="40">
                        <v-img
                          :alt="product.titulo"
                          :src="product.src"
                        ></v-img>
                      </v-list-item-avatar>
                      <v-list-item-content>
                        <v-list-item-title>{{product.titulo}}</v-list-item-title>
                        <v-list-item-subtitle class="text-subtitle-2 black--text">R$ {{real(product.valor_total)}} <!--{{product.descricao}}--></v-list-item-subtitle>
                        <v-list-item-subtitle v-if="product.msg === ''">
                          <v-btn
                            color="red darken-1"
                            outlined
                            x-small
                            @click="addmsg(product.id, product.titulo, product.msg), dialog2=true"
                          >
                            <v-icon
                              x-small
                              left  
                            >
                              mdi-comment-outline
                            </v-icon>
                            Observação
                          </v-btn>
                        </v-list-item-subtitle>
                        <v-list-item-subtitle v-else>
                          <strong>Obs:</strong> {{product.msg}}
                          <v-btn
                            x-small
                          >
                            <v-icon
                              color="red darken-1"
                              left
                              small
                              @click="addmsg(product.id, product.titulo, product.msg), dialog2=true"
                              
                            >
                              mdi-pencil
                            </v-icon>
                            
                          </v-btn>
                        </v-list-item-subtitle>
                      </v-list-item-content>
                      <v-list-item-action>
                        <v-list-item-action-text>
                          <v-btn
                          x-small
                          dark
                          depressed
                          fab
                          color="red"
                          @click="decrement(product.id, product.unidade, product.estoque, product.valor , product.valor_total)"
                          >
                            <v-icon
                              x-small  
                            >
                              mdi-minus
                            </v-icon>
                          </v-btn>
                          <span class="title">{{product.unidade}}</span>
                          <v-btn
                            x-small
                            dark
                            depressed
                            fab
                            color="green"
                            @click="increment(product.id, product.unidade, product.estoque, product.valor , product.valor_total)"
                          >
                            <v-icon
                              x-small  
                            >
                              mdi-plus
                            </v-icon>
                          </v-btn>
                        </v-list-item-action-text>
                      </v-list-item-action>  
                    </v-list-item>
                  </v-list>
                  <v-divider></v-divider>
                </v-card-text>
                <!--{{exibecarrinho()}} - {{productpage}}-->
                <v-card-actions>  
                  <v-spacer></v-spacer>
                    Total: <span class="title">R$ {{valorcarrinho}}</span>
                  <v-spacer></v-spacer>
                </v-card-actions>
                <v-card-actions>  
                  <v-btn
                    class="white--text"
                    color="red darken-1"                    
                    @click="dialog = false"
                    rounded
                    large
                  >
                    <v-icon left>mdi-cart-plus</v-icon>
                    Pedir mais
                  </v-btn>
                  <v-spacer></v-spacer>
                  
                  <v-spacer></v-spacer>
                  <v-btn
                    class="white--text"
                    color="black darken-1"                    
                    @click="dialog3 = true"
                    rounded
                    large
                  >
                    <v-icon left>mdi-cart-check</v-icon>
                    Finalizar
                  </v-btn>
                </v-card-actions>
                <div style="flex: 1 1 auto;"></div>
              </v-card>
            </v-dialog>
            <v-dialog
              v-model="dialog2"
              transition="dialog-bottom-transition"
              max-width="400"
            >              
              <v-card>
                <v-toolbar
                  flat
                  dark
                  color="red"
                >
                  <v-spacer></v-spacer>
                  <v-toolbar-title>{{titulo_msg}}</v-toolbar-title>                  
                  <v-spacer></v-spacer>
                  <v-btn
                    icon
                    dark
                    @click="dialog2 = false"
                  >
                    <v-icon>mdi-close</v-icon>
                  </v-btn>
                </v-toolbar>
                <v-card-text>
                  <br/>
                  <div class="justify-center">
                    <v-textarea
                      outlined
                      name="input-7-4"
                      :label="'Deixe aqui sua observação para '+titulo_msg"
                      v-model="mensagem_msg"
                    ></v-textarea>
                  </div>  
                </v-card-text>
                <v-card-actions class="justify-center">
                  <div class="justify-center">                      
                    <v-btn
                      class="white--text"
                      color="red darken-1"
                      x-large

                      @click="updatemsg(id_msg, mensagem_msg)"
                    >
                      <v-icon
                        left  
                      >
                        mdi-check
                      </v-icon>
                      Confirmar
                    </v-btn>                  
                  </div>
                </v-card-actions>
              </v-card> 
            </v-dialog>
            <v-dialog
              v-model="dialog3"
              fullscreen
              hide-overlay
              transition="dialog-bottom-transition"
            >
              <v-card tile>
                <v-toolbar
                  dark
                  color="red"
                >
                  <v-btn
                    icon
                    dark
                    @click="dialog3 = false"
                  >
                    <v-icon>mdi-chevron-left</v-icon>
                  </v-btn>
                  <v-toolbar-title>Dados da entrega</v-toolbar-title>                  
                </v-toolbar>
                <v-card-text>
                  <v-list
                    three-line
                    subheader
                  >                     
                    <v-subheader><v-icon left small>mdi-hand-coin</v-icon>Escolha uma opção de entrega <!--{{opcaoentrega}}--></v-subheader>
                    <v-item-group v-model="opcaoentrega">
                      <v-container>
                        <v-row>
                          <v-col
                            cols="4"
                            md="4"
                          >
                            <v-item v-slot="{ active, toggle }">
                              <v-card
                                :color="active ? 'red' : ''"
                                class="d-flex align-center"
                                dark
                                height="100"
                                @click="toggle"
                              >
                                <v-scroll-y-transition>
                                  <div
                                    v-if="active"
                                    class="flex-grow-1 text-center"
                                  >
                                    <v-icon>
                                      mdi-google-maps
                                    </v-icon>
                                    <br/>
                                    Entrega
                                    <br/>
                                    <span class="caption">
                                      <v-icon small>
                                        mdi-clock-outline
                                      </v-icon>  
                                      20-30 min
                                    </span>
                                  </div>
                                  <div
                                    v-else
                                    class="flex-grow-1 text-center"
                                  >
                                    <v-icon>
                                      mdi-google-maps
                                    </v-icon>
                                    <br/>
                                    Entrega
                                    <br/>
                                    <span class="caption">
                                      <v-icon small>
                                        mdi-clock-outline
                                      </v-icon>
                                      20-30 min
                                    </span>
                                  </div>
                                </v-scroll-y-transition>
                              </v-card>
                            </v-item>
                          </v-col>
                          <v-col
                            cols="4"
                            md="4"
                          >
                            <v-item v-slot="{ active, toggle }">
                              <v-card
                                :color="active ? 'red' : ''"
                                class="d-flex align-center"
                                dark
                                height="100"
                                @click="toggle"
                              >
                                <v-scroll-y-transition>
                                  <div
                                    v-if="active"
                                    class="flex-grow-1 text-center"
                                  >
                                    <v-icon>
                                      mdi-store
                                    </v-icon>
                                    <br/>
                                    Retirada
                                    <br/>
                                    <span class="caption">
                                      <v-icon small>
                                        mdi-clock-outline
                                      </v-icon>
                                      10-20 min
                                    </span>
                                  </div>
                                  <div
                                    v-else
                                    class="flex-grow-1 text-center"
                                  >
                                    <v-icon>
                                      mdi-store
                                    </v-icon>
                                    <br/>
                                    Retirada
                                    <br/>
                                    <span class="caption">
                                      <v-icon small>
                                        mdi-clock-outline
                                      </v-icon>
                                      10-20 min
                                    </span>
                                  </div>
                                </v-scroll-y-transition>
                              </v-card>
                            </v-item>
                          </v-col>
                          <v-col
                            cols="4"
                            md="4"
                          >
                            <v-item v-slot="{ active, toggle }">
                              <v-card
                                :color="active ? 'red' : ''"
                                class="d-flex align-center"
                                dark
                                height="100"
                                @click="toggle"
                              >
                                <v-scroll-y-transition>
                                  <div
                                    v-if="active"
                                    class="flex-grow-1 text-center"
                                  >
                                    <v-icon>
                                      mdi-table-chair
                                    </v-icon>
                                    <br/>
                                    Mesa
                                    <br/>
                                    <span class="caption">
                                      <v-icon small>
                                        mdi-clock-outline
                                      </v-icon>
                                      10-20 min
                                    </span>
                                  </div>
                                  <div
                                    v-else
                                    class="flex-grow-1 text-center"
                                  >
                                    <v-icon>
                                      mdi-table-chair
                                    </v-icon>
                                    <br/>
                                    Mesa
                                    <br/>
                                    <span class="caption">
                                      <v-icon small>
                                        mdi-clock-outline
                                      </v-icon>
                                      10-20 min
                                    </span>
                                  </div>
                                </v-scroll-y-transition>
                              </v-card>
                            </v-item>
                          </v-col>
                        </v-row>
                      </v-container>
                    </v-item-group>
                  </v-list>                    
                  <v-form
                    ref="form"
                    v-model="valid"
                    lazy-validation
                  >
                    <template v-if="opcaoentrega === 0 || opcaoentrega === 1">
                    
                     
                      <template v-if="opcaoentrega === 0">
                        <v-subheader><v-icon left small>mdi-google-maps</v-icon> Endereço da entrega</v-subheader>
                        <v-select
                          outlined
                          v-model="bairro"
                          :items="bairrolist"
                          :rules="bairroRules"
                          label="Bairro (Obrigatório)"
                          required
                        ></v-select>
                        
                        <v-text-field
                          outlined
                          v-model.trim="rua"
                          :counter="80"
                          :rules="ruaRules"
                          label="Rua (Obrigatório)"
                          required
                        ></v-text-field>

                        <v-text-field
                          outlined
                          v-model.trim="numero"
                          :rules="numeroRules"
                          :counter="6"
                          v-mask="'######'"
                          label="Número (Obrigatório)"
                          required
                        ></v-text-field>
                        
                        <v-text-field
                          outlined
                          v-model.trim="complemento"
                          :counter="20"
                          label="Complemento"
                          required
                        ></v-text-field>
                        <!--
                        <v-text-field
                          outlined
                          v-model="name"
                          :counter="10"
                          :rules="nameRules"
                          label="Ponto de Referência"
                          required
                        ></v-text-field>                     
                        -->
                        </template>
                    
                  
                    <v-subheader><v-icon left small>mdi-account</v-icon> Dados do cliente</v-subheader>
                    <v-text-field
                      outlined
                      v-model.trim="nome"
                      :counter="80"
                      :rules="nomeRules"
                      label="Nome do cliente (Obrigatório)"
                      required
                    ></v-text-field>

                    <v-text-field
                      outlined
                      v-model="telefone"
                      :counter="15"
                      :rules="telefoneRules"
                      label="Whatsapp com DDD (Obrigatório)"
                      required
                      v-mask="'(##) #####-####'"
                    ></v-text-field>
                    
                    <v-subheader><v-icon left small>mdi-currency-usd</v-icon> Forma de pagamento <!--{{opcaoformapgto}}--></v-subheader>
                    <v-item-group v-model="opcaoformapgto">
                      <v-container>
                        <v-row>
                          <v-col
                            cols="4"
                            md="4"
                            @click="dialog4 = true"
                          >
                            <v-item v-slot="{ active, toggle }">
                              <v-card
                                :color="active ? 'red' : ''"
                                class="d-flex align-center"
                                dark
                                height="80"
                                @click="toggle"
                              >
                                <v-scroll-y-transition>
                                  <div
                                    v-if="active"
                                    class="flex-grow-1 text-center"
                                  >
                                    <v-icon>
                                      mdi-cash
                                    </v-icon>
                                    <br/>
                                    Dinheiro
                                    <br/>
                                    <span v-if="troco_pagamento != '' " class="caption">
                                      troco para {{troco_pagamento}}
                                    </span>
                                    
                                  </div>
                                  <div
                                    v-else
                                    class="flex-grow-1 text-center"
                                  >
                                    <v-icon>
                                      mdi-cash
                                    </v-icon>
                                    <br/>
                                    Dinheiro
                                    
                                  </div>
                                </v-scroll-y-transition>
                              </v-card>
                            </v-item>
                          </v-col>
                          <v-col
                            cols="4"
                            md="4"
                          >
                            <v-item v-slot="{ active, toggle }">
                              <v-card
                                :color="active ? 'red' : ''"
                                class="d-flex align-center"
                                dark
                                height="80"
                                @click="toggle"
                              >
                                <v-scroll-y-transition>
                                  <div
                                    v-if="active"
                                    class="flex-grow-1 text-center"
                                  >
                                    <v-icon>
                                      mdi-credit-card-outline
                                    </v-icon>
                                    <br/>
                                    Cartão
                                    
                                  </div>
                                  <div
                                    v-else
                                    class="flex-grow-1 text-center"
                                  >
                                    <v-icon>
                                      mdi-credit-card-outline
                                    </v-icon>
                                    <br/>
                                    Cartão
                                    
                                  </div>
                                </v-scroll-y-transition>
                              </v-card>
                            </v-item>
                          </v-col>
                          <v-col
                            cols="4"
                            md="4"
                          >
                            <v-item v-slot="{ active, toggle }">
                              <v-card
                                :color="active ? 'red' : ''"
                                class="d-flex align-center"
                                dark
                                height="80"
                                @click="toggle"
                              >
                                <v-scroll-y-transition>
                                  <div
                                    v-if="active"
                                    class="flex-grow-1 text-center"
                                  >
                                    <v-icon>
                                      mdi-rhombus-split
                                    </v-icon>
                                    <br/>
                                    Pix
                                    
                                  </div>
                                  <div
                                    v-else
                                    class="flex-grow-1 text-center"
                                  >
                                    <v-icon>
                                      mdi-rhombus-split
                                    </v-icon>
                                    <br/>
                                    Pix
                                    
                                    
                                  </div>
                                </v-scroll-y-transition>
                              </v-card>
                            </v-item>
                          </v-col>
                        </v-row>
                      </v-container>
                    </v-item-group>
                    <v-subheader>Adicionar Cupom<v-btn text @click="exibecupom=true" x-small><v-icon small class="primary--text">mdi-plus</v-icon></v-btn><span :class="`caption ${snackbarColorCupom}--text`">{{ textcupom }}</span></v-subheader>
                    <div v-if="exibecupom == true">
                      <div class="position-relative" style="max-width: 400px">
                        <v-otp-input
                          v-model="otp"
                          :length="lengthotp"
                          :disabled="disabledotp"
                          @finish="onFinish"
                        ></v-otp-input>
                        <v-overlay absolute :value="loading">
                          <v-progress-circular
                            indeterminate
                            color="primary"
                          ></v-progress-circular>
                        </v-overlay>
                      </div>
                    </div>
                    <v-dialog
                      v-model="dialog4"
                      transition="dialog-bottom-transition"
                      max-width="400"
                    >              
                      <v-card>
                        <v-toolbar
                          flat
                          dark
                          color="red"
                        >
                          <v-spacer></v-spacer>
                          <v-toolbar-title>
                            <v-spacer></v-spacer>
                            Precisa de troco para <span class="title">R$ {{valorcarrinho}}</span> ?
                            <v-spacer></v-spacer>
                          </v-toolbar-title>                  
                          <v-spacer></v-spacer>
                          <v-btn
                            icon
                            dark
                            @click="dialog4 = false, troco = false"
                          >
                            <v-icon>mdi-close</v-icon>
                          </v-btn>
                        </v-toolbar>
                        <v-card-text v-if="troco == true">
                          <br/>
                          <div class="justify-center">
                            <v-text-field
                              outlined
                              v-model="troco_pagamento"
                              :counter="10"
                              :rules="trocoRules"
                              label="Troco para quanto?"
                              required
                              v-mask="'R$ ###'"
                            ></v-text-field>
                            
                          </div>  
                        </v-card-text>
                        <v-card-text v-else>
                          <br/>
                          <v-row>
                            <v-col
                              cols="6"
                              md="6"
                            >
                              <v-item v-slot="{ active, toggle }">
                                <v-card
                                  :color="active ? 'red' : ''"
                                  class="d-flex align-center"
                                  dark
                                  height="80"
                                  @click="toggle, troco = true"
                                >
                                  <v-scroll-y-transition>
                                    <div
                                      v-if="active"
                                      class="flex-grow-1 text-center"
                                    >
                                      <v-icon>
                                        mdi-check
                                      </v-icon>
                                      <br/>
                                      Sim
                                      
                                    </div>
                                    <div
                                      v-else
                                      class="flex-grow-1 text-center"
                                    >
                                      <v-icon>
                                        mdi-check
                                      </v-icon>
                                      <br/>
                                      Sim
                                      
                                    </div>
                                  </v-scroll-y-transition>
                                </v-card>
                              </v-item>
                            </v-col>
                            <v-col
                              cols="6"
                              md="6"
                            >
                              <v-item v-slot="{ active, toggle }">
                                <v-card
                                  :color="active ? 'red' : ''"
                                  class="d-flex align-center"
                                  dark
                                  height="80"
                                  @click="toggle, dialog4 = false"
                                >
                                  <v-scroll-y-transition>
                                    <div
                                      v-if="active"
                                      class="flex-grow-1 text-center"
                                    >
                                      <v-icon>
                                        mdi-close
                                      </v-icon>
                                      <br/>
                                      Não
                                      
                                    </div>
                                    <div
                                      v-else
                                      class="flex-grow-1 text-center"
                                    >
                                      <v-icon>
                                        mdi-close
                                      </v-icon>
                                      <br/>
                                      Não
                                      
                                    </div>
                                  </v-scroll-y-transition>
                                </v-card>
                              </v-item>
                            </v-col>
                          </v-row>
                        </v-card-text>
                        <v-card-actions v-if="troco == true" class="justify-center">
                          <div class="justify-center">                      
                            <v-btn
                              class="white--text"
                              color="red darken-1"
                              x-large
                              @click="dialog4 = false"
                            >
                              <v-icon
                                left  
                              >
                                mdi-check
                              </v-icon>
                              Confirmar
                            </v-btn>                  
                          </div>
                        </v-card-actions>
                      </v-card> 
                    </v-dialog>
                  </template>
                  <template v-if="opcaoentrega === 2">
                    <v-subheader><v-icon left small>mdi-table-chair</v-icon>Receber na mesa</v-subheader>
                    <v-text-field
                      outlined
                      v-model="mesa"
                      :counter="2"
                      :rules="mesaRules"
                      v-mask="'##'"
                      label="Número da mesa (Obrigatório)"
                      required
                    ></v-text-field>                       
                  </template>  
                </v-form>
                </v-card-text>
                <!-- {{objetopedido}} {{exibecarrinho()}}-->
                <v-card-actions>        
                  <v-spacer></v-spacer>                                        
                    Total: <span class="title">R$ {{valorcarrinho}}</span> <span v-if="valorcarrinho_antigo != 0" class="caption text-decoration-line-through" v-text="valorcarrinho_antigo"></span> 
                  <v-spacer></v-spacer>

                </v-card-actions>
                <v-card-actions>                    
                  <v-btn
                    v-if="opcaoentrega === 0 || opcaoentrega === 1 || opcaoentrega === 2"
                    block
                    x-large
                    :disabled="!valid"
                    class="white--text"
                    color="green darken-1"                    
                    @click="adicionapedido(opcaoentrega, opcaoformapgto)"
                  >
                    <v-icon>mdi-check</v-icon> Finalizar
                  </v-btn>
                  
                </v-card-actions>
                <div style="flex: 1 1 auto;"></div>
              </v-card>
            </v-dialog>
          </v-col>
        </v-row>
        <v-snackbar
          v-model="snackbar"
          :color="snackbarColor"
          :timeout="2000"
          centered
          outlined
          elevation="24"
        >
          {{ text }}
        </v-snackbar>
      </v-card>
    </v-card>
        
    <v-main>       
      <v-container>
        <!--Nuxt /-->
      </v-container>
    </v-main>
    <v-footer
      padless
      fixed
    >
      <v-bottom-navigation
        background-color="red"
        color="white"
        grow
      >
        <v-btn depressed>
          <span class="white--text">Cardápio</span>
          <v-icon color="white">mdi-home</v-icon>
        </v-btn>
        <v-btn @click="linkexterno('tel:5521981352741')" depressed>
          <span class="white--text">Telefone</span>
          <v-icon color="white">mdi-phone</v-icon>
        </v-btn>
        <v-btn @click="linkexterno('https://api.whatsapp.com/send?phone=5521981352741&text=*OLÁ VIZINHO! GOSTARIA DE FAZER 1 PEDIDO*')" depressed>
          <span class="white--text">Whatsapp</span>
          <v-icon color="white">mdi-whatsapp</v-icon>
        </v-btn>
        <v-btn
          v-if="objetocarrinho.length >= 1"
          @click="dialog=true"
        >
          <span class="white--text">Carrinho</span>
          <v-badge
            :content="objetocarrinho.length"
            color="green"
          >
            <v-icon color="white">mdi-cart</v-icon>
          </v-badge>
        </v-btn>
        <!--
        <v-btn 
          v-else
          @click="dialog=true"
        >
          <span class="white--text">Carrinho</span>
          <v-icon color="white">mdi-cart</v-icon>
        </v-btn>
        -->
      </v-bottom-navigation>
    </v-footer>    
    
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      //Lista de objetos e pagamentos
      nome_opcoes_entrega: {0:'Entrega', 1:'Retirada', 2:'Mesa'},
      nome_opcoes_pagamento: {0:'Dinheiro', 1:'Cartão', 2:'Pix'},
      nome_opcoes_cupom: [
        {
          nome: 'VIZINHO10',
          valor: 10,
          situacao: true
        },
        {
          nome: 'VIZINHO20',
          valor: 20,
          situacao: true
        },
        {
          nome: 'VIZINHO50',
          valor: 50,
          situacao: false
        },
        {
          nome: 'VIZINHO80',
          valor: 80,
          situacao: false
        },  
      ],  
      //objetos entrega e pagamento
      opcaoentrega:[],
      opcaoformapgto: [],
      focus: false,
      //Início formulario
      formapgto: null,
      valid: true,
      //Dados do cliente
      nome: '',
      nomeRules: [
        v => !!v || 'O nome é obrigatório',
        v => (v && v.length >= 3) || 'O nome não pode ter menos que 3 letras',
      ],
      telefone: '',
      telefoneRules: [
        v => !!v || 'O Whatsapp é obrigatório',
        v => (v && v.length >= 15) || 'Digite um Whatsapp válido',
      ],
      //Dados da entrega
      bairro: null,
      bairrolist: ['Realengo', 'Padre Miguel', 'Bangu', 'Sulacap'],
      bairroRules: [
        v => !!v || 'O bairro é obrigatório',
      ],
      rua: '',
      ruaRules: [
        v => !!v || 'O nome da rua é obrigatório',
        v => (v && v.length >= 3) || 'O nome da rua não pode ter menos que 3 letras',
      ],
      numero: '',
      numeroRules: [
        v => !!v || 'O número é obrigatório',
      ],
      complemento: '',
      mesa: '',
      mesaRules: [
        v => !!v || 'O número da mesa é obrigatório',
      ],
      checkbox: false,
      //Fim formulario
      //Início dos Pedidos
      objetopedido:[],
      cupom:'',
      sub_total: 0,
      valor_total: 0,
      //Fim dos Pedidos
      //Início dos Produtos
      id_msg:'',
      titulo_msg:'',
      mensagem_msg:'',
      objetocarrinho:[],
      valorcarrinho:0,
      valorcarrinho_antigo:0,
      troco_pagamento:'',
      qntd: 1,
      //Fim dos Produtos
      //Início Diálogos
      dialog: false,
      dialog2: false,
      dialog3: false,
      dialog4: false,
      troco: false,
      //Fim Diálogos
      //Início CUPOM
      loading: false,
      disabledotp: false,
      snackbar: false,
      snackbarColor: 'default',
      snackbarColorCupom: 'default',
      otp: '',
      text: '',
      textcupom: '',
      lengthotp: 9,
      expectedOtp: 'VIZINHO10',
      exibecupom: false,
      //Fim CUPOM
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js',
      tab: null,
      productpage: null,
      tabs: [
        {
          title:'Combos',
          texto:'texto dos Combos',
          itens:[
            {
              id: 0,
              titulo:'PULSE + BATATA FRITA + REFRI LATA',
              descricao:'Pão, carne, molho, salada e batata palha',
              valor: '15.00',
              valor_total: '15.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 1,
              titulo:'ONIX + BATATA FRITA + REFRI LATA',
              descricao:'Pão, carne, queijo, presunto, molho, salada e batata palha',
              valor: '17.00',
              valor_total: '17.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 2,
              titulo:'ARGO + BATATA FRITA + REFRI LATA',
              descricao:'Pão, carne, ovo, queijo, presunto, molho, salada e batata palha',
              valor: '18.00',
              valor_total: '18.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 3,
              titulo:'COBALT + BATATA FRITA + REFRI LATA',
              descricao:'Pão, carne, ovo, queijo, presunto, calabresa, molho, salada e batata palha',
              valor: '19.00',
              valor_total: '19.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 4,
              titulo:'JETTA + BATATA FRITA + REFRI LATA',
              descricao:'Pão, carne, queijo, bacon, molho, salada e batata palha',
              valor: '18.50',
              valor_total: '18.50',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 5,
              titulo:'DUSTER + BATATA FRITA + REFRI LATA',
              descricao:'Pão, 2 carnes, ovo, queijo, calabresa, cheddar, salada e batata palha',
              valor: '20.00',
              valor_total: '20.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 6,
              titulo:'TRACKER + BATATA FRITA + REFRI LATA',
              descricao:'Pão, 3 carnes, 3 ovos, queijo, bacon, calabresa, presunto, cheddar, polenguinho, catupiry, salada e batata palha',
              valor: '28.00',
              valor_total: '28.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 7,
              titulo:'TIGGO + BATATA FRITA + REFRI LATA',
              descricao:'Pão, carne de picanha, bacon, cheddar',
              valor: '20.00',
              valor_total: '20.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 8,
              titulo:'HB20 + BATATA FRITA + REFRI LATA',
              descricao:'Pão, 2 carnes de picanha, molho, salada e batata palha',
              valor: '19.00',
              valor_total: '19.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 9,
              titulo:'TORO + BATATA FRITA + REFRI LATA',
              descricao:'Pão, 2 carnes de picanha, 2 queijos, bacon, molho, salada e batata palha',
              valor: '22.00',
              valor_total: '22.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 10,
              titulo:'NIVUS + BATATA FRITA + REFRI LATA',
              descricao:'Pão, carne de picanha, queijo, bacon, ovo, calabresa, molho, salada e batata palha',
              valor: '20.00',
              valor_total: '20.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 11,
              titulo:'CRUZE + BATATA FRITA + REFRI LATA',
              descricao:'Pão, 2 carnes, cheddar, salada e batata palha',
              valor: '19.00',
              valor_total: '19.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 12,
              titulo:'CIVIC + BATATA FRITA + REFRI LATA',
              descricao:'Pão, 2 carnes de picanha, 2 ovos, polenguinho, bacon, calabresa, presunto, molho, salada e batata palha',
              valor: '24.00',
              valor_total: '24.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
          ]
        },
        {
          title:'Lanches',
          texto:'texto dos Lanches',
          itens:[
            {
              id: 13,
              titulo:'PULSE',
              descricao:'Pão, carne, molho, salada e batata palha',
              valor: '5.00',
              valor_total: '5.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 14,
              titulo:'ONIX',
              descricao:'Pão, carne, queijo, presunto, molho, salada e batata palha',
              valor: '7.00',
              valor_total: '7.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 15,
              titulo:'ARGO',
              descricao:'Pão, carne, ovo, queijo, presunto, molho, salada e batata palha',
              valor: '8.00',
              valor_total: '8.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 16,
              titulo:'COBALT',
              descricao:'Pão, carne, ovo, queijo, presunto, calabresa, molho, salada e batata palha',
              valor: '9.00',
              valor_total: '9.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 17,
              titulo:'JETTA',
              descricao:'Pão, carne, queijo, bacon, molho, salada e batata palha',
              valor: '8.50',
              valor_total: '8.50',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 18,
              titulo:'DUSTER',
              descricao:'Pão, 2 carnes, ovo, queijo, calabresa, cheddar, salada e batata palha',
              valor: '10.00',
              valor_total: '10.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 19,
              titulo:'TRACKER',
              descricao:'Pão, 3 carnes, 3 ovos, queijo, bacon, calabresa, presunto, cheddar, polenguinho, catupiry, salada e batata palha',
              valor: '18.00',
              valor_total: '18.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 20,
              titulo:'TIGGO',
              descricao:'Pão, carne de picanha, bacon, cheddar',
              valor: '10.00',
              valor_total: '10.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 21,
              titulo:'HB20',
              descricao:'Pão, 2 carnes de picanha, molho, salada e batata palha',
              valor: '9.00',
              valor_total: '9.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 22,
              titulo:'TORO',
              descricao:'Pão, 2 carnes de picanha, 2 queijos, bacon, molho, salada e batata palha',
              valor: '12.00',
              valor_total: '12.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 23,
              titulo:'NIVUS',
              descricao:'Pão, carne de picanha, queijo, bacon, ovo, calabresa, molho, salada e batata palha',
              valor: '10.00',
              valor_total: '10.00',
              unidade: 1,
              estoque: 10, 
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 24,
              titulo:'CRUZE',
              descricao:'Pão, 2 carnes, cheddar, salada e batata palha',
              valor: '9.00',
              valor_total: '9.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 25,
              titulo:'CIVIC',
              descricao:'Pão, 2 carnes de picanha, 2 ovos, polenguinho, bacon, calabresa, presunto, molho, salada e batata palha',
              valor: '14.00',
              valor_total: '14.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
          ]
        },
        {
          title:'Açai',
          texto:'texto dos açai',
          itens:[
            {
              id: 26,
              titulo:'AÇAÍ 200 ml',
              descricao:'Açaí 200 ml',
              valor: '5.00',
              valor_total: '5.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 27,
              titulo:'AÇAI 330 ml',
              descricao:'Açaí 330 ml',
              valor: '6.00',
              valor_total: '6.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 28,
              titulo:'AÇAI 440 ml',
              descricao:'Açaí 440 ml',
              valor: '8.00',
              valor_total: '8.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 29,
              titulo:'AÇAI 550 ml',
              descricao:'Açaí 550 ml',
              valor: '10.00',
              valor_total: '10.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
          ]
        },
        {
          title:'Aperitivos',
          texto:'texto dos Aperitivos',
          itens:[
            {
              id: 30,
              titulo:'BATATA FRITA',
              descricao:'Porção de batta frita',
              valor: '15.00',
              valor_total: '15.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 31,
              titulo:'BATATA FRITA COM CALABRESA',
              descricao:'Porção de batata frita com calabresa',
              valor: '25.00',
              valor_total: '25.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 32,
              titulo:'FRANGO À PASSARINHO',
              descricao:'Porção de frango à passarinho',
              valor: '25.00',
              valor_total: '25.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 33,
              titulo:'SALAMINHO ITALIANO',
              descricao:'Porção de salaminho Italiano',
              valor: '15.00',
              valor_total: '15.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 34,
              titulo:'CARNE SECA COM AIPIM',
              descricao:'Porção de carne seca com aipim',
              valor: '30.00',
              valor_total: '30.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 35,
              titulo:'OVOS DE CODORNA COM AZEITONAS',
              descricao:'Porção de ovos de codorna com azeitonas',
              valor: '15.00',
              valor_total: '15.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 36,
              titulo:'ANEL DE CEBOLA',
              descricao:'Porção de anel de cebola',
              valor: '12.00',
              valor_total: '12.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 37,
              titulo:'SARDINHA',
              descricao:'Porção de sardinha',
              valor: '25.00',
              valor_total: '25.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 38,
              titulo:'CAMARÃO',
              descricao:'Porção de camarão',
              valor: '25.00',
              valor_total: '25.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 39,
              titulo:'FILÉ APERITIVO',
              descricao:'Porção de filé aperitivo',
              valor: '30.00',
              valor_total: '30.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 40,
              titulo:'AIPIM DA CASA',
              descricao:'Porção de aipim da casa',
              valor: '25.00',
              valor_total: '25.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            {
              id: 41,
              titulo:'BATATA MALUCA',
              descricao:'Batata, bacon, linguiça calabresa, frango à passarinho, queijo parmesão e queijo cheddar',
              valor: '30.00',
              valor_total: '30.00',
              unidade: 1,
              estoque: 10,
              src:'https://images.multipedidos.com.br/covers/c319bfd5446d492012d63277a75134190c7178db785b0cad895e6bef66fb2c95.jpg',
              msg:''
            },
            
          ]
        }
      ],
    }
  },
  methods: {
    onFinish (rsp) {
      rsp = rsp.toUpperCase();
      this.loading = true
      let valor = 0;
      const retorno = this.nome_opcoes_cupom.find( obj => obj.nome === rsp && obj.situacao === true)
      setTimeout(() => {
        this.loading = false
        if(retorno != undefined){
          this.snackbarColor = 'success'
          this.snackbarColorCupom = 'success'
          this.disabledotp = true
          //this.exibecupom = (rsp === this.expectedOtp) ? false : true
          this.cupom = retorno.nome
          this.text = `Cupom "${retorno.nome}" ativado com sucesso`
          this.textcupom = `Cupom "${retorno.nome}" ativado com sucesso`
          this.valorcarrinho_antigo = this.valorcarrinho
          valor = (parseFloat(this.valorcarrinho) - (parseFloat(this.valorcarrinho) * retorno.valor) / 100)
          this.valorcarrinho = valor.toLocaleString('pt-br', {minimumFractionDigits: 2})
        }else{
          this.snackbarColor = 'error'
          this.snackbarColorCupom = 'error'
          this.disabledotp = false
          //this.exibecupom = (rsp === this.expectedOtp) ? false : true
          this.text = 'Cupom inválido'
          this.textcupom = 'Cupom inválido'
        }        
        this.snackbar = true
      }, 3500);
    },
    addmsg(id, titulo, msg){
      this.id_msg = id;
      this.titulo_msg = titulo;
      this.mensagem_msg = msg; 
    },
    updatemsg(id, msg){
      this.objetocarrinho.find( obj => obj.id === id && ( obj.msg = msg, true ));
      this.dialog2 = false
    },
    decrement (id, unidade, estoque, preco, valor) {
      //this.qntd--;
      let atualiza_quantidade = parseFloat(unidade) + parseFloat(-1);
      if(atualiza_quantidade < 1){
        //this.qntd = 1;
        atualiza_quantidade = 1;
        this.objetocarrinho = this.objetocarrinho.filter(product => product.id != id);
        //let array = this.objetocarrinho.reduce((prev,next) => prev + parseFloat(next.valor),0);
        //this.valorcarrinho = array.toLocaleString('pt-br', {minimumFractionDigits: 2})
        if(Object.keys(this.objetocarrinho).length === 0){
          this.dialog = false
        }
        //
      }
      let atualiza_valor = parseFloat(preco) * parseFloat(atualiza_quantidade);
      this.objetocarrinho.find( obj => obj.id === id && ( obj.unidade = atualiza_quantidade, obj.valor_total = parseFloat(atualiza_valor), true ));
      let array = this.objetocarrinho.reduce((prev,next) => prev + parseFloat(next.valor_total),0);
      this.valorcarrinho = array.toLocaleString('pt-br', {minimumFractionDigits: 2})     
      
      //this.cart(this.qntd, preco);
    },
    increment (id, unidade, estoque, preco, valor) {
      let atualiza_quantidade = parseFloat(unidade) + parseFloat(1);
      if(atualiza_quantidade >= estoque){
        atualiza_quantidade = estoque
      }
      let atualiza_valor = parseFloat(preco) * parseFloat(atualiza_quantidade);
      this.objetocarrinho.find( obj => obj.id === id && ( obj.unidade = atualiza_quantidade, obj.valor_total = parseFloat(atualiza_valor), true ));
      let array = this.objetocarrinho.reduce((prev,next) => prev + parseFloat(next.valor_total),0);
      this.valorcarrinho = array.toLocaleString('pt-br', {minimumFractionDigits: 2})     
      //this.cart(unidade, preco);
    },
    adicionacarrinho (obj){
      let cart_id = obj.id;
      let cart_titulo = obj.titulo;
      let cart_descricao = obj.descricao;
      let cart_valor = obj.valor;
      let cart_valor_total = obj.valor_total;
      let cart_estoque = obj.estoque;
      let cart_unidade = obj.unidade;
      let cart_src = obj.src;
      let cart_msg = obj.msg;
      if (this.objetocarrinho.map(x => x.id).indexOf(cart_id) === -1){
        this.objetocarrinho.push({id:cart_id, titulo:cart_titulo, descricao:cart_descricao, valor:cart_valor, valor_total:cart_valor_total, unidade:cart_unidade, estoque:cart_estoque, src:cart_src, msg:cart_msg})
        let array = this.objetocarrinho.reduce((prev,next) => prev + parseFloat(next.valor_total),0);
        this.valorcarrinho = array.toLocaleString('pt-br', {minimumFractionDigits: 2})  
      }                  
      //this.objetocarrinho.push({id:'1',qntd:'qntd'})
    },
    adicionapedido (modo_entrega, forma_pagamento){
      let tempo_min_entrega = 0
      let tempo_max_entrega = 0
      if(modo_entrega === 0){
        tempo_min_entrega = 20
        tempo_max_entrega = 30
      }else{
        tempo_min_entrega = 10
        tempo_max_entrega = 20
      }
      this.objetopedido = [];
      let pedido_bairro = this.bairro;
      let pedido_rua = this.rua;
      let pedido_numero = this.numero;
      let pedido_complemento = this.complemento;
      let pedido_nome = this.nome;
      let pedido_telefone = this.telefone;
      let pedido_modo_entrega = modo_entrega;
      let pedido_pagamento = forma_pagamento;
      let pedido_troco_pagamento = this.troco_pagamento;
      let pedido_mesa = this.mesa;
      let pedido_carrinho = this.objetocarrinho;
      //let pedido_valor_carrinho = this.valorcarrinho;
      let pedido_sub_total = (this.valorcarrinho_antigo != 0 ) ? this.valorcarrinho_antigo : this.valorcarrinho
      let pedido_valor_total = this.valorcarrinho;
      let pedido_cupom = this.cupom;
      let pedido_tempo_entrega = this.formataTempoEntrega(new Date(), tempo_min_entrega, tempo_max_entrega);
      let pedido_data = this.formataDataPedido(new Date());
      if(modo_entrega === 0){ 
        if(pedido_pagamento === 0 && pedido_troco_pagamento != ""){
          this.objetopedido.push({
            bairro: pedido_bairro,
            rua: pedido_rua,
            numero: pedido_numero,
            complemento: pedido_complemento,
            nome: pedido_nome,
            telefone: pedido_telefone,
            modo_entrega: pedido_modo_entrega,
            tempo_entrega: pedido_tempo_entrega,
            pagamento: pedido_pagamento,
            carrinho: pedido_carrinho,
            //valor_carrinho: pedido_valor_carrinho,
            troco_pagamento: pedido_troco_pagamento,
            sub_total: pedido_sub_total,
            valor_total: pedido_valor_total,
            cupom: pedido_cupom,
            data: pedido_data
          })    
        }else{
          this.objetopedido.push({
            bairro: pedido_bairro,
            rua: pedido_rua,
            numero: pedido_numero,
            complemento: pedido_complemento,
            nome: pedido_nome,
            telefone: pedido_telefone,
            tempo_entrega: pedido_tempo_entrega,
            modo_entrega: pedido_modo_entrega,
            pagamento: pedido_pagamento,
            carrinho: pedido_carrinho,
            //valor_carrinho: pedido_valor_carrinho,
            sub_total: pedido_sub_total,
            valor_total: pedido_valor_total,
            cupom: pedido_cupom,
            data: pedido_data
          })
        }
      }
      if(modo_entrega === 1){
        if(pedido_pagamento === 0 && pedido_troco_pagamento != ""){
          this.objetopedido.push({
            nome: pedido_nome,
            telefone: pedido_telefone,
            tempo_entrega: pedido_tempo_entrega,
            modo_entrega: pedido_modo_entrega,
            pagamento: pedido_pagamento,
            carrinho: pedido_carrinho,
            //valor_carrinho: pedido_valor_carrinho,
            troco_pagamento: pedido_troco_pagamento,
            sub_total: pedido_sub_total,
            valor_total: pedido_valor_total,
            cupom: pedido_cupom,
            data: pedido_data
          })    
        }else{
          this.objetopedido.push({
            nome: pedido_nome,
            telefone: pedido_telefone,
            tempo_entrega: pedido_tempo_entrega,
            modo_entrega: pedido_modo_entrega,
            pagamento: pedido_pagamento,
            carrinho: pedido_carrinho,
            //valor_carrinho: pedido_valor_carrinho,
            sub_total: pedido_sub_total,
            valor_total: pedido_valor_total,
            cupom: pedido_cupom,
            data: pedido_data
          })
        }    
      }
      if(modo_entrega === 2){
        this.objetopedido.push({
          modo_entrega: pedido_modo_entrega,
          mesa: pedido_mesa,
          tempo_entrega: pedido_tempo_entrega,
          carrinho: pedido_carrinho,
          //valor_carrinho: pedido_valor_carrinho,
          sub_total: pedido_sub_total,
          valor_total: pedido_valor_total,
          data: pedido_data
        })    
      }
      this.validapedido(modo_entrega, forma_pagamento);
      //this.whatsapp();
    },
    whatsapp(){
      let wpp_bairro = this.objetopedido[0].bairro;
      let wpp_rua = this.objetopedido[0].rua;
      let wpp_numero = this.objetopedido[0].numero;
      let wpp_complemento = this.objetopedido[0].complemento;
      let wpp_nome = this.objetopedido[0].nome;
      let wpp_telefone = this.objetopedido[0].telefone;
      let wpp_tempo_entrega = this.objetopedido[0].tempo_entrega;
      let wpp_modo_entrega = this.objetopedido[0].modo_entrega;
      let wpp_pagamento = this.objetopedido[0].pagamento;
      let wpp_modo_entrega_nominal = this.nome_opcoes_entrega[this.objetopedido[0].modo_entrega];
      let wpp_pagamento_nominal = this.nome_opcoes_pagamento[this.objetopedido[0].pagamento];
      let wpp_troco_pagamento = this.objetopedido[0].troco_pagamento;
      let wpp_mesa = this.objetopedido[0].mesa;
      let wpp_carrinho = "";
      let wpp_valor_item_carrinho = 0;
      let wpp_sub_total_item_carrinho = 0; 
      let wpp_objeto_carrinho = this.objetopedido[0].carrinho.forEach(function(value, key){wpp_valor_item_carrinho = parseFloat(value.valor); wpp_sub_total_item_carrinho = parseFloat(value.valor_total); wpp_carrinho += `*${value.unidade}x* ${value.titulo} ${value.msg} - R$ ${wpp_valor_item_carrinho.toLocaleString('pt-br', {minimumFractionDigits: 2})} unidade%0ASubtotal do item - *R$ ${wpp_sub_total_item_carrinho.toLocaleString('pt-br', {minimumFractionDigits: 2})}*%0A%0A`});
      //let pedido_valor_carrinho = this.valorcarrinho;
      let wpp_sub_total = this.objetopedido[0].sub_total;
      let wpp_valor_total = this.objetopedido[0].valor_total;
      let wpp_cupom = this.objetopedido[0].cupom;
      let wpp_data = this.objetopedido[0].data;
      //Entrega
      if(wpp_modo_entrega === 0){ 
        if(wpp_pagamento === 0 && wpp_troco_pagamento != ""){
          return window.location.href = `https://api.whatsapp.com/send?phone=5521981352741&text=*VIZINHO'S HAMBURGUERIA DELIVERY*%0A-------------------------------------------------%0A*RESUMO DO PEDIDO:* ${wpp_data}%0A-------------------------------------------------%0A%0A${wpp_carrinho}-------------------------------------------------%0A*SUBTOTAL = R$ ${wpp_sub_total}*%0A-------------------------------------------------%0A%0A*DADOS DA ENTREGA*%0A%0A*Nome:* ${wpp_nome}%0A*Endereço:* ${wpp_rua}, ${wpp_numero} - ${wpp_bairro} ${wpp_complemento}%0A*Telefone:* ${wpp_telefone}%0A*Tempo aprox. de entrega:* ${wpp_tempo_entrega}%0A-------------------------------------------------%0A%0A*VALOR TOTAL = R$ ${wpp_valor_total}* (${wpp_pagamento_nominal}) ${wpp_cupom}%0A*TROCO PARA:* ${wpp_troco_pagamento}`
        }else{
          return window.location.href = `https://api.whatsapp.com/send?phone=5521981352741&text=*VIZINHO'S HAMBURGUERIA DELIVERY*%0A-------------------------------------------------%0A*RESUMO DO PEDIDO:* ${wpp_data}%0A-------------------------------------------------%0A%0A${wpp_carrinho}-------------------------------------------------%0A*SUBTOTAL = R$ ${wpp_sub_total}*%0A-------------------------------------------------%0A%0A*DADOS DA ENTREGA*%0A%0A*Nome:* ${wpp_nome}%0A*Endereço:* ${wpp_rua}, ${wpp_numero} - ${wpp_bairro} ${wpp_complemento}%0A*Telefone:* ${wpp_telefone}%0A*Tempo aprox. de entrega:* ${wpp_tempo_entrega}%0A-------------------------------------------------%0A%0A*VALOR TOTAL = R$ ${wpp_valor_total}* (${wpp_pagamento_nominal}) ${wpp_cupom}`
        }
      }
      //Retirada na Loja
      if(wpp_modo_entrega === 1){
        if(wpp_pagamento === 0 && wpp_troco_pagamento != ""){
          return window.location.href = `https://api.whatsapp.com/send?phone=5521981352741&text=*VIZINHO'S HAMBURGUERIA DELIVERY*%0A-------------------------------------------------%0A*RESUMO DO PEDIDO:* ${wpp_data}*%0A-------------------------------------------------%0A%0A${wpp_carrinho}-------------------------------------------------%0A*SUBTOTAL = R$ ${wpp_sub_total}*%0A-------------------------------------------------%0A%0A*RETIRADA NA LOJA*%0A%0A*Nome:* ${wpp_nome}%0A*Telefone:* ${wpp_telefone}%0A*Tempo aprox. de entrega:* ${wpp_tempo_entrega}%0A-------------------------------------------------%0A*VALOR TOTAL = R$ ${wpp_valor_total}* (${wpp_pagamento_nominal}) ${wpp_cupom}%0A%0A*TROCO PARA:* ${wpp_troco_pagamento}`     
        }else{
          return window.location.href = `https://api.whatsapp.com/send?phone=5521981352741&text=*VIZINHO'S HAMBURGUERIA DELIVERY*%0A-------------------------------------------------%0A*RESUMO DO PEDIDO:* ${wpp_data}*%0A-------------------------------------------------%0A%0A${wpp_carrinho}-------------------------------------------------%0A*SUBTOTAL = R$ ${wpp_sub_total}*%0A-------------------------------------------------%0A%0A*RETIRADA NA LOJA*%0A%0A*Nome:* ${wpp_nome}%0A*Telefone:* ${wpp_telefone}%0A*Tempo aprox. de entrega:* ${wpp_tempo_entrega}%0A-------------------------------------------------%0A*VALOR TOTAL = R$ ${wpp_valor_total}* (${wpp_pagamento_nominal}) ${wpp_cupom}`
        }    
      }
      //Entrega na Mesa
      if(wpp_modo_entrega === 2){
        return window.location.href = `https://api.whatsapp.com/send?phone=5521981352741&text=*VIZINHO'S HAMBURGUERIA DELIVERY*%0A-------------------------------------------------%0A*RESUMO DO PEDIDO:* ${wpp_data}*%0A-------------------------------------------------%0A%0A${wpp_carrinho}-------------------------------------------------%0A*SUBTOTAL = R$ ${wpp_sub_total}*%0A-------------------------------------------------%0A%0A*ENTREGA NA MESA*%0A%0A*Mesa:* ${wpp_mesa}%0A*Tempo aprox. de entrega:* ${wpp_tempo_entrega}%0A-------------------------------------------------%0A*VALOR TOTAL = R$ ${wpp_valor_total}*`   
      }
    },
    validapedido(modo_entrega, forma_pagamento){
      if(modo_entrega === 0 || modo_entrega === 1 || modo_entrega === 2){
      
        let acertos = 0
        if(modo_entrega === 0){
          acertos = 0
          if(this.bairro != null){
            acertos ++
          }else{
            this.snackbarColor = 'error'
            this.text = 'O campo Bairro deve ser preenchido'
            this.snackbar = true
            //alert("O campo Bairro deve ser preenchido");
          }
          if(this.rua.length > 3 ){
            acertos ++
          }else{
            this.snackbarColor = 'error'
            this.text = 'O campo Rua deve ser preenchido'
            this.snackbar = true
            //alert("O campo Rua deve ser preenchido ");
          }
          if(this.numero != "" || this.numero > 0){
            acertos ++
          }else{
            this.snackbarColor = 'error'
            this.text = 'O campo Número deve ser preenchido'
            this.snackbar = true
            //alert("O campo número deve ser preenchido");
          }
          if(this.nome.length > 3 ){
            acertos ++
          }else{
            this.snackbarColor = 'error'
            this.text = 'O campo Nome deve ser preenchido'
            this.snackbar = true
            //alert("O campo nome deve ser preenchido");
          } 
          if(this.telefone.length === 15 ){
            acertos ++
          }else{
            this.snackbarColor = 'error'
            this.text = 'O campo Telefone deve ser preenchido'
            this.snackbar = true
            //alert("O campo telefone deve ser preenchido");
          }
          if(forma_pagamento === 0 || forma_pagamento === 1 || forma_pagamento === 2){
            acertos ++
          }else{
            this.snackbarColor = 'error'
            this.text = 'A forma de pagamento deve ser escolhida'
            this.snackbar = true
            //alert("A forma de pagamento deve ser escolhida ");
          }
          if(acertos === 6){
            //alert("Tudo certo podem festejar!!!");
            this.whatsapp();
          }
        }else{
          this.snackbarColor = 'error'
          this.text = 'O modo de entrega deve ser escolhido'
          this.snackbar = true
          //alert("A forma de pagamento deve ser escolhida ");
        }  
      
        if(modo_entrega === 1){
          acertos = 0
          if(this.nome.length > 3 ){
            acertos ++
          }else{
            this.snackbarColor = 'error'
            this.text = 'O campo nome deve ser preenchido'
            this.snackbar = true
            //alert("O campo nome deve ser preenchido");
          } 
          if(this.telefone.length === 15 ){
            acertos ++
          }else{
            this.snackbarColor = 'error'
            this.text = 'O campo telefone deve ser preenchido'
            this.snackbar = true
            //alert("O campo telefone deve ser preenchido");
          }
          if(forma_pagamento === 0 || forma_pagamento === 1 || forma_pagamento === 2){
            acertos ++
          }else{
            this.snackbarColor = 'error'
            this.text = 'A forma de pagamento deve ser escolhida'
            this.snackbar = true
            //alert("A forma de pagamento deve ser escolhida");
          }
          if(acertos === 3){
            //alert("Tudo certo podem festejar!!!");
            this.whatsapp();
          }
        }
      
        if(modo_entrega === 2){
          acertos = 0
          if(this.mesa > 0 || this.mesa != ""){
            acertos ++
          }else{
            this.snackbarColor = 'error'
            this.text = 'A mesa deve ser escolhida'
            this.snackbar = true
            //alert("A mesa deve ser escolhida");
          }
          if(acertos === 1){
            //alert("Tudo certo podem festejar!!!");
            this.whatsapp();
          }
        }
      }else{
        this.snackbarColor = 'error'
        this.text = 'Como deseja receber: entrega, retirada ou mesa'
        this.snackbar = true
        //alert("A forma de pagamento deve ser escolhida ");
      }
    },
    formataTempoEntrega(data, min, max){
      //let data = new Date()
      let tempo_min = new Date(data.getTime() + min * 60000)
      let tempo_max = new Date(data.getTime() + max * 60000)
      let min_min = tempo_min.getMinutes()
      let hora_min = tempo_min.getHours()
      let min_max = tempo_max.getMinutes()
      let hora_max = tempo_max.getHours()
      return hora_min+":"+min_min+" a "+hora_max+":"+min_max
    },  
    formataDataPedido(obj){
      let date = obj
      let arraymeses = ["01", "02", "03", "04", "05", "06", "07", "08", "09", "10", "11", "12"];
      let ano = date.getFullYear()
      let mes = arraymeses[date.getMonth()]
      let dia = date.getDate()
      let hor = date.getHours()
      let min = date.getMinutes()
      let seg = date.getSeconds()
      return ano+mes+dia+hor+min+seg
    },
    linkexterno(obj){
      return window.open(obj)  
    },
    mostratroco(formapgto){
      this.dialog4=true;
    },
    exibecarrinho (obj){
      return this.objetocarrinho
    },
    real (preco){
      let valor = parseFloat(preco);
      return valor.toLocaleString('pt-br', {minimumFractionDigits: 2})
    },
  }
}
</script>
<style scoped>
 .position-relative {
   position: relative;
 }
 .v-btn--example {
    bottom: 0;
    position: absolute;
    margin: 0 0 16px 16px;
  }
</style>