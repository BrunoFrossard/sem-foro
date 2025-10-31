##### Bruno Frossard Silva, Grupo 1 - T18


## Projeto Semáforo - Controle de Fluxo de Trânsito


#### Descrição do Projeto

Este projeto teve como objetivo desenvolver um semáforo funcional para controle de fluxo de trânsito no bairro Butantã, utilizando Arduino, LEDs e componentes eletrônicos básicos. O sistema implementa a lógica temporal padrão de um semáforo convencional.

### 1. Montagem Física do Semáforo

##### 1.1 Componentes Utilizados

| Componente | Quantidade | Especificação | Função |
|------------|------------|---------------|--------|
| LED Azul | 1 | 5mm, 2V, 20mA | Sinal de parada |
| LED Amarelo | 1 | 5mm, 2V, 20mA | Sinal de atenção |
| LED Verde | 1 | 5mm, 2V, 20mA | Sinal de passagem |
| Resistor | 3 | 220Ω, 1/4W | Limitação de corrente |
| Protoboard | 1 | 830 pontos | Base de montagem |
| Jumpers | Diversos | Macho-Macho | Conexões |
| Arduino | 1 | Uno R3 | Controlador |

##### 1.2 Esquema de Montagem

**Conexões Realizadas:**

1. **LED Azul:**
   - Anodo (perna longa) → Resistor 220Ω → Pino Digital 13 do Arduino
   - Catodo (perna curta) → GND

2. **LED Amarelo:**
   - Anodo (perna longa) → Resistor 220Ω → Pino Digital 12 do Arduino
   - Catodo (perna curta) → GND

3. **LED Verde:**
   - Anodo (perna longa) → Resistor 220Ω → Pino Digital 11 do Arduino
   - Catodo (perna curta) → GND

##### 1.3 Imagens da Montagem

![Esquema de Conexões do Semáforo](assets\i1.jpeg)
*Figura 1: Primeira parte do código*

![Montagem Completa na Protoboard - Vista Frontal](assets\i2.jpeg)
*Figura 2: Montagem física completa na protoboard - vista frontal*

![Parte do Loop do código](assets\i3.jpeg)
*Figura 3: Segunda parte do código*

##### 1.4 Justificativas Técnicas

**Escolha dos Resistores:**
Os resistores de 200Ω foram calculados considerando a tensão de alimentação do Arduino (5V) e a tensão típica dos LEDs (2V), resultando em uma corrente de aproximadamente 13,6mA, valor seguro que protege os LEDs sem comprometer o brilho.

**Disposição dos LEDs:**
Os LEDs foram dispostos verticalmente na protoboard, simulando a configuração real de um semáforo de trânsito, facilitando a visualização e teste do sistema.

### 2. Programação do Semáforo

### 2.1 Código Implementado
```cpp
class Semaforo {
  private:
    int pinoAzul;
    int pinoAmarelo;
    int pinoVerde;
    int tempoAzul;
    int tempoAmarelo;
    int tempoVerde;
    
  public:
    Semaforo(int pAzul, int pAmarelo, int pVerde) {
      pinoAzul = pAzul;
      pinoAmarelo = pAmarelo;
      pinoVerde = pVerde;
      tempoAzul = 6000;  
      tempoAmarelo = 2000;   
      tempoVerde = 4000;
    }
    
    void inicializar() {
      pinMode(pinoAzul, OUTPUT);
      pinMode(pinoAmarelo, OUTPUT);
      pinMode(pinoVerde, OUTPUT);
      apagarTodos();
    }
    
    void apagarTodos() {
      digitalWrite(pinoAzul, LOW);
      digitalWrite(pinoAmarelo, LOW);
      digitalWrite(pinoVerde, LOW);
    }
    
    void faseAzul() {
      apagarTodos();
      digitalWrite(pinoAzul, HIGH);
      delay(tempoAzul);
    }
    
    void faseVerde() {
      apagarTodos();
      digitalWrite(pinoVerde, HIGH);
      delay(tempoVerde);
    }
    
    void faseAmarela() {
      apagarTodos();
      digitalWrite(pinoAmarelo, HIGH);
      delay(tempoAmarelo);
    }
    
    void executarCiclo() {
      faseVermelha();
      faseVerde();
      faseAmarela();
    }
    
    void configurarTempos(int* tAzul, int* tVerde, int* tAmarelo) {
      if (tVermelho != nullptr) {
        tempoAzul = *tAzul;
      }
      if (tVerde != nullptr) {
        tempoVerde = *tVerde;
      }
      if (tAmarelo != nullptr) {
        tempoAmarelo = *tAmarelo;
      }
    }
    
    void obterTempos(int* tAzul, int* tVerde, int* tAmarelo) {
      if (tAzul != nullptr) {
        *tAzul = tempoAzul;
      }
      if (tVerde != nullptr) {
        *tVerde = tempoVerde;
      }
      if (tAmarelo != nullptr) {
        *tAmarelo = tempoAmarelo;
      }
    }
};


Semaforo* ptrSemaforo;

void setup() {
  ptrSemaforo = new Semaforo(2, 4, 3);
  
  ptrSemaforo->inicializar();
  
 
}

void loop() {
  ptrSemaforo->executarCiclo();
}
```

### 2.2 Lógica Implementada

O semáforo foi programado para operar em um ciclo contínuo com a seguinte temporização:

- **Azul:** 6 segundos
- **Verde:** 4 segundos
- **Amarelo:** 2 segundos
- **Ciclo Total:** 12 segundos |

### 3. Demonstração em Vídeo

**Link do Vídeo:** [Vídeo da Montagem Física](assets\video.mp4)

### 4. Avaliações de Pares

###### Avaliador 1

**Nome do Avaliador:** [Nome Completo do Avaliador 1]

Nota:

**Comentários Gerais:**
[Comentários do avaliador 1]

###### Avaliador 2

**Nome do Avaliador:** [Nome Completo do Avaliador 2]

Nota:

**Comentários Gerais:**
[Comentários do avaliador 2]

### 5. Conclusão

O projeto opera o semáforo corretamente seguindo a temporização especificada, a montagem física está organizada e segura, e a documentação completa permite a reprodução do projeto.

