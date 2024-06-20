<h1><b>Jogo-da-forca-v2</b></h1> 

## Objetivo
O objetivo do presente projeto foi o desenvolvimento de um jogo da forca simples com uma espécie de tabuleiro definido, utilizando a '<a href=https://github.com/mathwatanabe/Jogo-da-forca-v1>Versão 1</a>' como base. O intuito principal do trabalho foi o aprimoramento e aprofundamento na prática de conceitos e técnicas da linguagem Python. Além disso, uma das principais competências utilizadas foi a transformação dos dados de um arquivo do tipo csv em um objeto do tipo dicionário em Python. Outro conceito importante foi a utilização do pacote <code>random</code> e o aprofundamento na construção de funções. Dessa forma, o foco do projeto não foi a construção de um código otimizado, com menor tempo de execução ou simplificação, mas sim para o aperfeiçoamento e desenvolvimento de habilidades e competências referentes à linguagem Python.

## Ferramentas
* Python 3.10.13

## Desenvolvimento
Foi utilizado o dicionário de palavras produzido na versão 1. A produção desse dicionário está explicada e definida nela.

O primeiro passo foi importar a biblioteca <code>random</code> que foi utilizada para selecionar um item aleatório do dicionário e foi importado o pacote <code>os</code> para a criação de uma função responsável por limpar a tela.
```neon
import random
from os import system, name
def limpa_tela():
    if name == 'nt':
        _ = system('cls')
    else:
        _ = system('clear')
```
A grande diferença com a versão 1 desse jogo é o tabuleiro. O tabuleiro é representado por um boneco que incialmente é montado cada elemento do seu rosto, representado pelos itens de índice de 6 a 13. De 0 a 5 é representado o corpo do boneco sendo montado. E, por último, o índice 14 seria o rosto do boneco sem vida, que equivaleria ao usuário perder o jogo. Cada item foi associado a uma quantidade específica de tentivas restantes do usuário.
```neon
def forca(numero_tentativas):
    estagio = [
    '''    -------------
    |           |
    |
    |
    |               
    |
    -''',
    '''    -------------
    |           |
    |           O
    |
    |               
    |
    -''',
    ...
    #Cada imagem do tabuleiro associada a um índice da lista acima
    if numero_tentativas == 14:
        print(estagio[0])
        return
    elif numero_tentativas == 13:
        print(estagio[6])
        return
```

Posteriormente foi criada uma função capaz de substituir, nas palavras que possuem acento, a letra acentuada pela letra sem a marcação gráfica. Isso foi necessário para que o usuário não necessitasse diferenciar as letras acentuadas ou não acentuadas, e para o programa não ter diferenciação entre a letra acentuada ou não. O resto do código pode ser encontrado no arquivo '<a href=https://github.com/mathwatanabe/Jogo-da-forca-v2/blob/main/Jogo-da-forca-v2.py>Jogo-da-forca-v2.py</a>'
```neon
def substituir(palavra):
    #Essa variável será a palavra escolhida do dicionário de forma aleatória posteriormente
    palavra = str(palavra)
    #A função lower() foi utilizada para não necessitar da diferenciação entre letras no início da palavra ou no meio
    palavra2 = palavra.lower()
    if 'á' in palavra2:
        palavra2 = palavra2.replace('á','a')
    if 'â' in palavra:
        palavra2 = palavra2.replace('â','a')
    if 'ã' in palavra:
        palavra2 = palavra2.replace('ã','a')
```
Uma função para a criação automática de um gabarito, no qual, as letras eram substituídas por '_'.
```neon
def letras_palavra(charada):
    memoria_resposta = []
    #A variável charada serve para serve para receber a palavra a ser adivinhada
    for letra in charada:
        #Se a palavra possuir algum dos caracteres abaixo, eles não serão substituídos por '_'
        if letra == '-' or letra == ')' or letra == '(' or letra == '.' or letra == ' ' or letra == ',':
            memoria_resposta.append(letra)
        elif letra == '1' or letra == '2' or letra == '3' or letra == '4' or letra == '5' or letra == '6' or letra == '7' or letra == '8' or letra == '9' or letra == '0':
            memoria_resposta.append(letra)
        #As letras são substituídas por '_'
        else:
            memoria_resposta.append('_')
    return memoria_resposta
```
Por fim, foi criado o bloco de código responsável pela dinâmica do jogo. Mais detalhes acerca do código podem ser encontrados em '<a href=https://github.com/mathwatanabe/Jogo-da-forca-v2/blob/main/Jogo-da-forca-v2.py>Jogo-da-forca-v2.py</a>'. Em resumo, a função <code>choice</code> foi chamada para realizar a escolha aleatória no dicionário contendo as palavras a serem adivinhadas.
```neon
def game():
    #Execução da limpeza de tela
    limpa_tela()
    dicionário_palavras = {'Brasil': 'Países', 'Estados Unidos': 'Países', 'China': 'Países', 'Índia': 'Países', 'Japão': 'Países', ..., 'Ozark': 'Séries Famosas'}
    #Guardando a palavra definida aleatoriamente pela função choice() do pacote random
    palavra1, grupo = random.choice(list(dicionário_palavras.items()))
```
Foram realizados 3 passos importantes, a criação de uma lista para guardar as letras incorretas que foram escolhidas, definição de uma variável <code>tentativas</code> para guardar a quantidade de tentativas restantes do usuário e a utilização da função <code>substituir()</code> definida anteriormente para retirar os acentos das palavras.
```neon
def game():
    ...

    #Uma lista é definida para gravar as letras erradas já escolhidas
    letras_erradas = []
    tentativas = int
    
    #Retirar os acentos da palavra escolhida para ser adivinhada
    palavra_sem_acento = substituir(palavra1)
```
Foi definida a quantidade de tentativas fixa em 14.
```neon
def game():
    ...

  #Definição da quantidade máxima de tentativas para cada grupo de palavras específico
  tentativas = 14

    #Definir a quantidade de '_' que irão aparecer no gabarito da palavra
    m = letras_palavra(palavra1)
```
Por último o bloco de execução principal para apresentar informações importantes para o usuário foi definido, como as seguintes informações, tabuleiro, quantidade de tentativas, gabarito com as letras corretas já adivinhadas e letras incorretas. Além disso, esse bloco mantém um loop até que o usuário tenha ganhado ou tenha perdido por não ter mais tentativas. Para verificar se o usuário ganhou, o condicional if é utilizado para verificar a existência do caracter '_' no gabarito, se não houver, isso significa que o usuário adivinhou todas as letras palavra.
```neon
def game():
    ...

    while tentativas > 0:
        #Para verificar se todas as letras foram adivinhadas
        if '_' not in m:
            #Se não houver, então o usuário ganhou o jogo
            print(f'----------\nᕦ( ͡° ͜ʖ ͡°)ᕤ\nVocê ganhou! A resposta é {palavra1}.')
            return
        print('\n----------\n')
        #Chamada da função forca para determinar o estado do tabuleiro
        forca(tentativas)
        #Mostrar o gabarito na tela
        print(' '.join(m))
        #Mostrar quantidade de tentativas
        print(f'Você ainda tem {tentativas} tentativas.')
        #Mostrar a letras erradas
        print('Letras erradas:',' '.join(letras_erradas))
```
Ainda no loop <code>while</code>, o pedido de inserção e verificação da letra inserida foi definido como representado abaixo. O condicional foi utilizado para, enquanto o usuário não inserisse uma letra válida no programa ou se ele inserisse uma letra incorreta já tentada, ele permaneceria pedindo a inserção da letra.
```neon
def game():
    ...

        #Pedir ao usuário a inserção de uma letra
        letra = input('Insira uma letra: ')
        #Essa condicional serve para não aceitar caracteres inválidos
        if len(letra) != 1 or letra == 'â' or letra == 'ã' or letra == 'é' or letra == 'ê' or letra == 'í' or letra == 'î' or letra == 'ó' or letra =='ô' or letra == 'ú' or letra == 'û':
            continue
        #Se a letra inserida já estiver sido tentada, mas não estiver na palavra, o loop recomeça
        elif letra.upper() in letras_erradas:
            continue
```
O bloco de código utilizado quando uma letra correta fosse inserida. Nele, a letra correta substituiria no gabarito o caracter '_' pela letra correta adivinhada.
```neon
def game():
    ...

        #Se a letra escolhida estiver na palavra, segue essa condicional
        elif letra.lower() in palavra_sem_acento.lower():
            print(f'A letra "{letra.upper()}" está na palavra!')
            #Verificar e substituir onde a letra escolhida de forma correta será colocada
            for i in range(0,len(palavra1)):
                #Comparar a letra minúscula com a palavra apenas com letras minúsculas para não ocorrer erro de comparação entre maiúscula e minúscula
                if letra.lower() == palavra_sem_acento.lower()[i]:
                    #Substituir o '_' no gabarito pela letra correta
                    m[i] = letra.upper()
                else:
                    continue
```
Por último, se fosse inserida uma letra incorreta, a parte representada abaixo seria responsável por identificar e tratar tal erro, reduzindo o número de tentivas e adicionando a letra errada na lista de letras erradas.
```neon
def game():
    ...

        #Se a letra escolhida não estiver na palavra e ainda não tiver sido verificada
        elif letra.lower() not in palavra_sem_acento.lower():
            #Reduzir o número de tentativas em 1
            tentativas -= 1
            #Adicionar a letra errada à lista de letras incorretas
            letras_erradas.append(letra.upper())
            print(f'A letra "{letra.upper()}" não está na palavra!')
            #Verificar se ainda há tentativas
            if tentativas == 0:
                #Se não houver mais tentativas, mostrar que a situação do tabuleiro e uma mensagem que o usuário perdeu
                forca(tentativas)
                print(f'----------\nVocê perdeu! A resposta era {palavra1}')
```
Com o código para execução do jogo finalizado, os blocos foram executados conforme demonstrado abaixo:
```neon
if __name__ == "__main__":
    game()
    print('Até a próxima!')
```
