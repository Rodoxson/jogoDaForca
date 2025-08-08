# Jogo da Forca - Projeto em Java

![Jogo da Forca](./images/pngegg.png)
 *Imagem ilustrativa do jogo da forca*

---

## Índice

- [Descrição](#descrição)  
- [Tecnologias](#tecnologias)  
- [Instalação](#instalação)  
- [Como Jogar](#como-jogar)  
- [Arquitetura do Projeto](#arquitetura-do-projeto)  
- [Estrutura de Código](#estrutura-de-código)  
- [Exemplo de Execução](#exemplo-de-execução)  
- [Progressão do Boneco](#progressão-do-boneco)  
- [Script de Testes Automáticos](#script-de-testes-automáticos)  
- [Contribuições](#contribuições)  
- [Licença](#licença)  

---

## Descrição

Este projeto é uma implementação do clássico **Jogo da Forca** em Java, utilizando estrutura de dados e manipulação de strings para criar uma experiência interativa no terminal.

O objetivo do jogo é que o jogador tente adivinhar uma palavra secreta, letra por letra, antes que o boneco da forca seja completamente desenhado.

---

## Tecnologias

- Java 17  
- Maven (para gerenciamento de dependências e build)  
- Terminal/Console  

---

## Instalação

1. Clone este repositório:  
   ```bash
   git clone https://github.com/seu-usuario/jogo-da-forca-java.git
   cd jogo-da-forca-java

2. Compile o projeto:
   ```bash
      mvn clean compile

3. Execute o Jogo:
   ```bash
      mvn exec:java -Dexec.mainClass="dio.br.com.Main" -Dexec.args="PALAVRA"

Substitua PALAVRA pela palavra que deseja que o jogador adivinhe.

## Como Jogar
  . Ao iniciar, você será apresentado ao desenho da forca com espaços para a palavra secreta.

  . Escolha uma das opções:

        1. Informar uma letra

        2. Verificar Status do jogo

        3. Sair do jogo

  . Informe letras e tente adivinhar a palavra antes que o boneco seja desenhado completamente.

## Arquitetura do Projeto
```plaintext
  src/
├── dio/
│   └── br/
│       └── com/
│           ├── model/
│           │   ├── HangmanGame.java        # Lógica principal do jogo
│           │   ├── HangmanChar.java        # Representação das letras e peças do boneco
│           │   └── HangmanGameStatus.java  # Enum dos estados do jogo (PENDING, WIN, LOSE)
│           ├── exception/
│           │   ├── GameIsFinishedException.java
│           │   └── LetterAlreadyInputedException.java
│           └── Main.java                    # Classe principal com interface do jogo
```

## Estrutura de Código

### HangmanGame.java
. Responsável por controlar o estado do jogo, processar entradas, atualizar o desenho e verificar vitória/derrota.

. Usa LinkedList para controlar as partes do boneco da forca.

. Calcula dinamicamente as posições dos caracteres no desenho para evitar desalinhamentos.

### HangmanChar.java
. Representa um caractere do jogo: letra da palavra ou parte do boneco.

. Mantém visibilidade para saber se a letra já foi descoberta.

### HangmanGameStatus.java
. Enum com os estados possíveis do jogo:

. PENDING (jogo em andamento)

. WIN (vitória)

. LOSE (derrota)

### Exceções personalizadas
. GameIsFinishedException — lançada quando o usuário tenta jogar após o fim do jogo.

. LetterAlreadyInputedException — lançada ao tentar informar uma letra já digitada.

## Exemplo de Execução
```plaintext
. Bem vindo ao jogo da forca, tente adivinhar a palavra, boa sorte!

  -----  
  |   |
  |   |
  |      
  |      
  |      
=========

Selecione uma das opções:
1 - Informar uma letra
2 - Verificar Status do jogo
3 - Sair do jogo

Digite uma letra:

a

  -----  
  |   |
  |   |
  |   O   
  |      
  |      
=========

Tentativas erradas: [a]
```
## Progressão do Boneco
```plaintext
  -----  
  |   |
  |   |    O
  |   |   /|\
  |   |   / \
  |
=========

| Tentativas | Partes do Boneco   |   |
| ---------- | ------------------ |   |
| 1          | Cabeça   O         |   |
| 2          | Tronco   |         |   |
| 3          | Braço esquerdo /   |   |
| 4          | Braço direito \    |   |
| 5          | Perna esquerda /   |   |
| 6          | Perna direita \    |   |
```

## Script de Testes Automáticos
. Para facilitar testes automatizados do jogo, você pode usar o script abaixo que simula tentativas de letras, incluindo erros e acertos.

```java
package dio.br.com;

import dio.br.com.model.HangmanChar;
import dio.br.com.model.HangmanGame;
import dio.br.com.model.HangmanGameStatus;

import java.util.List;

public class HangmanTest {

    public static void main(String[] args) {
        String palavra = "teste";
        List<HangmanChar> chars = palavra.chars()
                .mapToObj(c -> new HangmanChar((char) c, false, 0))
                .toList();

        HangmanGame jogo = new HangmanGame(chars);

        // Letras para tentar (algumas certas, outras erradas)
        char[] tentativas = {'a', 'e', 't', 'x', 's', 'z', 'o'};

        for (char c : tentativas) {
            try {
                jogo.inputCharacter(c);
                System.out.println("Tentando letra: " + c);
                System.out.println(jogo);
            } catch (Exception ex) {
                System.out.println(ex.getMessage());
            }
            if (jogo.getHangmanGameStatus() != HangmanGameStatus.PENDING) {
                System.out.println("Jogo finalizado com status: " + jogo.getHangmanGameStatus());
                break;
            }
        }
    }
}



## Contribuições

### Contribuições são bem-vindas!

. Fork este projeto

. Crie uma branch para sua feature (git checkout -b feature/minha-feature)

. Faça commit das suas alterações (git commit -m 'Minha nova feature')

. Envie para o repositório remoto (git push origin feature/minha-feature)

. Abra um Pull Request

## Licença
. Este projeto está licenciado sob a licença MIT. Veja o arquivo LICENSE para mais detalhes.










