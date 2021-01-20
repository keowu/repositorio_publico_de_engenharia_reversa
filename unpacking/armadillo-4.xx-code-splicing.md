---
description: >-
  Alvo: Anti Tracks v5.6.1   | ARM 4.xx-Code Splicing | Livro traduzido:
  Team-REA
---

# Armadillo 4.xx-Code Splicing

![Livro do Team-REA](../.gitbook/assets/capturar.png)

Nesse tutorial você vai precisar das seguintes ferramentas:

* OllyDBG - Com a melhor configuração para debbug para ArmMUP do hacnho
* LordPE 1.4 Deluxe
* Import REConstructor 1.6 Final
* ArmInline 0.6

Você pode adaptar para a nova geração com as seguintes configurações:

* x96Dbg - Com SharpOD ou qualquer outro Anti-Debug de sua preferência
* Scylla Dump

## **Iniciando o Unpacking**

Carregue o alvo

![](../.gitbook/assets/2.png)

Avance até o **GetModuleHandleA**, use o shift + F9 chegar até a função e para ignorar as exceções

![](../.gitbook/assets/3.png)

Pressione novamente shift + F9, por duas vezes

![](../.gitbook/assets/4.png)

Pressione novamente shift + F9, por três vezes

![](../.gitbook/assets/5.png)

Enter 4:

![](../.gitbook/assets/6.png)

Enter 5:

![](../.gitbook/assets/8.png)

Enter 6:

![](../.gitbook/assets/9.png)

Enter 7:

![](../.gitbook/assets/10.png)

Enter 8:

![](../.gitbook/assets/11.png)

Enter 9:

![](../.gitbook/assets/12.png)

Tecla F8 para navegar através do opcode RETN, você terá a seguinte visão:

![](../.gitbook/assets/13.png)

Salto mágico, EB's patch:

![](../.gitbook/assets/14.png)

Avance até o GetModuleHandle A, defina um breakpoint "BP CreateThread", continue com Shift + F9, Ctrl + F9, F8, Ctrl + F9, F8:

![](../.gitbook/assets/15.png)

Aperte Down

![](../.gitbook/assets/16.png)

Esse "CALL EDI", Breakpoint com F2, F9, F7 e Pronto chegamos ao OEP!

![](../.gitbook/assets/17.png)

Precisamos encontrar sinais de código para fazer uma emenda, use ALT + M:

![](../.gitbook/assets/18.png)

Vamos ao ArmInline completar as informações como a seguir:

![](../.gitbook/assets/19.png)

Hehe, Nossa emenda foi um sucesso, vamos encontrar a IAT, No endereço 00401022, se você  seguir no dump você vai encontrar informações da IAT como a seguir:

| IAT | Informação |
| :--- | :--- |
| Inicio da IAT | 004837FC 4000A314 **VCL50. System @ @ initialization $ qqrv** |
| Fim da IAT | 00484FE8 7621F6C6 **WININET.FindNextUrlCacheEntryA** |
| Tamanho da IAT | 000017EC |

Vamos dumpar com o LordPE:

![](../.gitbook/assets/20.png)

Entre com as seguintes informações no impREC:

| Tipo | Endereço |
| :--- | :--- |
| OEP | 00001000 |
| IATRVA | 000837FC |
| IATSIZE | 000017EC |

![](../.gitbook/assets/21.png)

Sobre nosso DUMP:

![](../.gitbook/assets/22.png)

Vamos detectar nosso DUMP usando o PeiD 0.93:

![](../.gitbook/assets/23.png)

Vamos rodar nosso DUMP:

![](../.gitbook/assets/24.png)

