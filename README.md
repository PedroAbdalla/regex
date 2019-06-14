# regex
exemplos de expressões regulares

nomes 
. ponto
[] lista
[^] lista negada
? opcinal
* asterisco
+ mais
{} chaves
^ circunflexo
$ cifrão
\b borda
\ scape
| ou
() grupo
\1 retrovisor


Representantes

. ponto => Um caracter qualquer
[...] lista => Lista de caracteres permitidos
[^...] lista negada => Lista de caracteres proibidos

Quantificadores

? opcinal => zero ou um
* asterisco => zero ou um ou mais
+ mais =>  um ou mais
{n,m} chaves =>  de n até m

Âcoras

^ circunflexo => Início da linha
$ cifrão => Fim da linha
\b borda => I´nicio ou fim da palavra

Outros

\c scape => Torne literal o caractere c
| ou => Ou um ou Outro
(...) grupo => Delimita um grupo
\1... \9 retrovisor => Texto casado nos grupos 1...9

REPRESENTANTES

____ . ponto ____

Ponto é o coringa, pode ser qualquer caracter
Exemplo:

n.o => não; nao;
.eclado => teclado; Teclado;
12.45 => 12:45; 12 45; 12.45;

____ [...] Lista ____

Lista so casa com seus póropios elementos
dentro da lista, todo mundo é normal!!!!

n[ãa]o => nao; não;
[Tt]eclado => teclado, Teclado;
12[:. ]45 => 12:45; 12 45; 12.45;

- traço, representa intervalo, logo
[0123456789]é igual [0-9]

exemplo lista letras maiusculas, minusculas e numeros
[A-Za-z0-9]

pegar colchete que fecha deve ficar sempre em primeiro em uma lista
pegar traço  deve ficar sempre em ultimo em uma lista

[]0] , [0-9-]


inclui acentuação
[[:upper:]] letras maiusculas
[[:lower:]] letras minusculas
[[:alnum:]] letras e numeros
[[:alpha:]] maiusculas e minusculas

____ [^...] Lista Negada ____

Ela possui lógica inversa, ou seja, ela casará com qualquer coisa, fora os componentes listados.
A lista negada sempre deve casar algo.
[^[:alpha:]] tudo que nao for letra

____ Metacaracteres tipo Quantificador ____

Dizem a quantidade de repetições que o átomo anterior pode ter, quantas vezes ele pode aparecer.

_____ ? Opcional _____
pode ter ou não a ocorrência da entidade anterior

***** leia a ER átomo por átomo, da esquerda para a direita.*******
ondas? => onda, ondas
fala[r!]? => fala; fala!; falar;


Lista e Opcional

</?[BIPbip]>    </B>, </I>, </P>, </b>, </i>, </p>, <B>, <I>, <P>, <b>, <i>, <p>
</?[BIPbip]?>    </B>, </I>, </P>, </b>, </i>, </p>, <B>, <I>, <P>, <b>, <i>, <p>, </>
fala[r!]? => fala; fala!; falar;

_____ * Asterisco _____

para ele pode ter, não ter, ou ter vários, infinitos. Em outras palavras, a entidade anterior pode aparecer em qualquer quantidade.

6*0         0, 60, 660, 6660, ..., 666666666660, ...
bi*p        bp, bip, biip, biiip, biiiip...
</?[BIPbip] *>  </B>, </B >, </B  >, ..., <p         >,

*** * Asterisco é guloso
[ar]* => arara   [ar] quatro vezes (a,r,a,r), seguido de a, logo retorna arara.

___ curinga .* ____

retorna qualquer coisa,

essa er retorna qualquer coisa, qualquer coisa mesmo!!!
er.*coisa =>  er retorna qualquer coisa, qualquer coisa

_____ + Mais ______
A única diferença do asterisco é que o mais não é opcional, então a entidade anterior deve casar pelo menos uma vez, e pode ter várias.

bi+p => bip, biip, biiip, biiiip
bi*p => bp, bip, biip, biiip, biiiip

___ {n,m} Chaves _____
6{1,4} => 6, 66, 666 e 6666

_____ Metacaracteres tipo Âncora _____

 eles não casam caracteres ou definem quantidades, ao invés disso eles marcam uma posição específica na linha.

 ____ ^ Circunflexo ______
circunflexo marca o começo de uma linha. Nada mais.

retoro o inicio da uma **linha** q começa com numeros
^[0-9] => {
5pppppp; 
3gnjeng; 
1 
0efwefw
}

retoro o inicio da uma **linha** q não começa com numeros
Só é especial no começo da ER.
^[0-9] => {
a556pppppp; 
agn54jeng74; 
a 
aef47wefw
}

____ $ Cifrão _____
cifrão marca o fim de uma linha e só é válido no final de uma ER.

^$ => retorna uma linha vazia
^.{20,60}$ => retorna uma linha entre 20 e 60 caracteres

____ \b Borda _____
marca uma borda, mais especificamente, uma borda de palavra.
na maioria das linguagens uma palavra engloba [A-Za-z0-9_]

dia      =>   dia, diafragma, radial, melodia, bom-dia!
\bdia    =>   dia, diafragma, bom-dia!
dia\b    =>   dia, melodia, bom-dia!
\bdia\b  =>   dia, bom-dia!

____ \ Escape _____

O escape escapa um metacaractere, tirando seu poder.
\* = [*] = asterisco literal.

____ | Ou ____
emelhante a lista porem compara palavras

boa tarde|boa Noite   => boa tarde, boa noite
http://|ftp:// => http://, ftp://

(...) Grupo
O grupo tem o dom de jutar vários tipos de sujeitos em um mesmo local
(ha!)+           =>   ha!, ha!ha!, ha!ha!ha!, ...
(\.[0-9]){3}     =>   .0.6.2, .2.8.9, .6.6.6, ...
(www\.)?zz\.com  =>   www.zz.com, zz.com
((su|hi)per)?mercado => supermercado, hipermercado, mercado

_____\1 Retrovisor_______
retrovisor busca um grupo casado anteriormente

((((a)b)c)d)-1 = \1,\2,\3,\4    abcd-1 = abcd,abc,ab,a
 ([0-9])\1 casa 66 mas não 69.
([A-Za-z]+)-?\1 => quero-quero, queroquero, bombom

Para não se perder nas contagens, há uma dica valiosa: conte somente os parênteses que abrem, da esquerda para a direita. Este vai ser o número do retrovisor. E o conteúdo é o texto casado pela ER do parêntese que abre até seu correspondente que fecha.

O retrovisor referencia o texto casado e não a ER do grupo.

O retrovisor só funciona se usado com o grupo.

Quantificadores não-gulosos
só casa se o próximo átomo da ER não estiver precisando daquele caractere. Veja a comparação entre ambos os tipos de gulodice em todos os quantificadores:
gulosos
*sempre vai caar o menor possível;
---------------------
a.*      =>   aaaaa
a.+      =>   aaaaa
a.?      =>   aa
a.{1,3}  =>   aaaa

não-gulosos
---------------------
a.*?      =>  a
a.+?      =>  aa
a.??      =>  a
a.{1,3}?  =>  aa


___________linguagens modernas______________
______Metacaracteres tipo barra-letra_______

b-l POSIX equiv.    mnemônico
-------------------------------------------
\d  [[:digit:]]     dígito
\D  [^[:digit:]]    não-dígito
\w  [[:alnum:]_]    palavra
\W  [^[:alnum:]_]   não-palavra
\s  [[:space:]]     branco
\S  [^[:space:]]    não-branco

exemplo rg
[0-9]\.[0-9]{3}\.[0-9]{3}-[0-9]]
ou
\d\.\d{3}\.\d{3}-\d


____(?#texto) comentarop

para fazer um comentario
(?#o nome)Homer (?#e agora o sobrenome)Simpson  Homer Simpson

_____(?:ER)____
É como um grupo normal () só que não é guardado nem incluído na contagem de grupos, ou seja, não é acessível com retrovisores 


(?=ER)

Não casa caracteres na posição atual, mas dá uma "espiada" adiante e caso a ER embutida case, retorna sucesso. É como só apostar na loteria se você já souber o resultado. Por exemplo a ER Homer (?=Simpson) só casará o Homer se for seguido de Simpson. Mas o sobrenome não faz parte do trecho casado, serviu apenas para checagem.

(?!ER)
É o contrário do anterior, só casando um trecho se este não for seguido da ER embutida. 

(?<=ER) (?<!ER)
Estes dois são complementares aos dois anteriores, a diferença é que em vez de espiar para frente, eles espiam para trás

(?(condição)ER-sim|ER-não) ??????


_____negar palavra___

^( [^a] | a[^q] | aq[^u] | aqu[^i] )  -- nega a apalarva aqui no inicio
(?!aqui) -- modernos


***Negar uma palavra, só no começo ou fim da linha.*****
***Há como negar uma ou mais palavras, em apenas alguns aplicativos.****
