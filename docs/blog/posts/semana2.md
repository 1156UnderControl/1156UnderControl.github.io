| date       | authors                 |
|------------|-------------------------|
| 2025-07-30 | Enzo Coutinho, Kalsing |

## Semana 2

### Novidades da comunidade

Na última semana, a comunidade FRC continuou debatendo o SystemCore.  Um dos tópicos mais comentados no fórum Chief Delphi discutiu a ausência de suporte oficial a sistemas Linux.  Vários membros defenderam que uma nova geração de controladores deve permitir o desenvolvimento em ambientes diversos e que disponibilizar ferramentas compatíveis com Linux reduziria a necessidade de máquinas virtuais e melhoraria a integração com ferramentas modernas de desenvolvimento.  Ainda não houve um posicionamento oficial, mas a discussão ilustra o interesse da comunidade em recursos avançados.

Outro fio de discussão (“SystemCore Alpha Test Blog”) reuniu equipes que estão testando as unidades alpha e apresentando resultados preliminares.  Os relatos indicam que a plataforma está estável e que a API de programação evolui rapidamente, embora ainda haja detalhes a serem refinados.  A participação intensa mostra o engajamento dos times no processo de validação.

### Atualizações da FIRST

Em comunicado oficial publicado pela FIRST em 19 de março de 2025, a organização informou que os testes de hardware do SystemCore seguem dentro do cronograma.  O controlador tem dimensões semelhantes a um smartphone grande e apresenta um conjunto robusto de conexões: cinco portas CAN‑FD, seis portas SmartIO, duas portas I²C, quatro portas USB‑A 3.0, USB‑C, Ethernet e entrada de alimentação, além de saída de luz de status (RSL) e porta para a ponte MotionCore【131986501979202†L23-L63】.  Entre os recursos integrados destacam‑se um sensor inercial (IMU), um slot M.2 para adicionar um acelerador de IA Hailo‑8 e conectividade Wi‑Fi integrada【131986501979202†L23-L63】.  O software também avança: a interface web do SystemCore permite configurar o dispositivo, programar diretamente no robô (com Blockly, Java ou Python) e visualizar valores de sensores; os testes no evento com o Field Management System mostraram funcionamento adequado【131986501979202†L70-L83】.  A FIRST reforça que o objetivo é reduzir barreiras de entrada sem comprometer as capacidades avançadas que as equipes experientes desejam.

### Testes do Under Control

Na última semana a nossa equipe prosseguiu com os testes alpha utilizando a unidade do SystemCore.  Os experimentos e anotações foram registrados no Notion e no repositório SystemCore_AlphaTest.

**Código vazio** –  O primeiro teste consistiu em carregar um projeto base sem lógica de controle para verificar se o ambiente de desenvolvimento e o fluxo de implantação estavam funcionando.  O objetivo foi criar um esqueleto de código que servirá de base para testes posteriores.  O resultado foi positivo: o controlador inicializou, as portas responderam conforme esperado e não houve falhas no upload ou na execução.

**PID de RPM com motor NEO** –  O segundo ensaio avaliou o PID interno de velocidade do SparkMax usando um motor NEO.  O código deste teste está disponível no branch `PID-RPM-Test` do repositório [`SystemCore_AlphaTest`](https://github.com/1156UnderControl/SystemCore_AlphaTest/tree/PID-RPM-Test).  O controlador conseguiu manter o RPM desejado, mas foi necessário adaptar o código porque o SystemCore não possui portas DIO de 5 V como o RoboRIO.  Como os sensores de efeito Hall do SparkMax usam sinal digital de 5 V, não foi possível conectá‑los diretamente; a solução foi utilizar somente o sensor interno do motor e ajustar a lógica para operar com portas de 3,3 V.  Os monitores de CAN mostraram um aumento de cerca de 1 % na utilização da rede durante o teste e, conforme esperado, um único motor não é suficiente para saturar a banda.  Nenhum erro foi registrado, indicando que, mesmo adaptando a interface, o SystemCore operou de forma estável.

### Próximos passos

A equipe continuará explorando os limites do novo controlador nas próximas semanas.  Estão planejados testes com múltiplos motores e sensores externos compatíveis com 3,3 V, bem como a validação de protocolos como CAN‑FD e a avaliação da interface web de programação.  Também acompanharemos de perto as publicações oficiais da FIRST e as discussões na comunidade para que nossas implementações estejam alinhadas com as melhores práticas.
