⚠️ Uso somente em redes e equipamentos para os quais você tenha autorização. O HÉRCULES observa o tráfego da interface em que está rodando.

🛡️ HÉRCULES NDR 
Cibersegurança · Monitoramento e triagem de tráfego de rede com apoio de IA local

Este repositório reúne a apresentação do HÉRCULES NDR, um projeto em Python que observa o tráfego de rede e ajuda o profissional de TI e de cibersegurança a separar o que é rotina do que merece uma olhada. Ele combina triagem determinística com uma IA executada localmente, que serve como segunda opinião. A análise crítica e as decisões de segurança continuam com a pessoa.

👉 [Assistir à demonstração no YouTube](https://www.youtube.com/watch?v=Aua-mBLTaoM)

Os dados exibidos no vídeo estão anonimizados.

🎯 Objetivos
Capturar e observar o tráfego de rede.
Aplicar critérios de triagem para organizar os eventos.
Usar IA local como segunda opinião quando necessário.
Apresentar informações que possam merecer investigação.
Manter o profissional humano no controle das decisões.

🧠 Como funciona
Captura: o TShark captura os metadados do tráfego (origem, destino, porta, protocolo e tamanho).
Triagem: regras em Python separam o tráfego de rotina e agrupam eventos repetidos, para reduzir a sobrecarga de informação.
Segunda opinião: eventos fora do padrão conhecido podem ser encaminhados à IA local (Ollama). A IA não analisa cada pacote capturado.
Aviso: o resultado aparece no terminal e, quando relevante, em uma janela de aviso. Quem decide o que fazer é o operador.

O HÉRCULES não bloqueia, não isola e não altera nada na rede. Um evento fora do padrão conhecido não é necessariamente malicioso.

⚙️ Tecnologias e requisitos
Python 3.10 ou superior
TShark (Wireshark)
Ollama, com um modelo de linguagem executado localmente
Tkinter (janelas de aviso)
Testado em Linux e Windows
🧪 Testes realizados

O projeto foi testado em ambientes Linux e Windows, incluindo condições de maior volume de tráfego.

Os resultados dependem do equipamento, da configuração, do modelo de IA e das condições de execução. A captura de eventos e a análise pela IA são etapas distintas: uma solicitação à IA pode falhar ou ficar pendente. Os testes não constituem garantia de detecção de todas as ameaças nem de ausência de perdas em qualquer ambiente.

Resultados observados

Sessão	Duração	Pacotes	Eventos observados	Encaminhados à IA
Windows, rede de maior porte (com autorização)	cerca de 3h13min	cerca de 300 mil	cerca de 17,9 mil	1
Linux, laboratório	cerca de 3h13min	26.775	1.601	6
Nas duas sessões, a triagem por regras tratou sozinha mais de 99% dos eventos observados.
Nessas sessões, nenhuma consulta à IA foi respondida dentro do tempo limite configurado. O modelo e o tempo limite são ajustáveis, e a IA é uma etapa complementar: a triagem por regras funciona sem ela.

🔐 Privacidade

O projeto foi concebido para usar IA local, sem depender de uma API de IA em nuvem para a análise complementar. A privacidade efetiva depende da configuração, das dependências e do tratamento dos registros.

Os registros gerados podem conter endereços IP de dispositivos da rede, inclusive de outras pessoas. Trate esses arquivos como dados pessoais e anonimize-os antes de compartilhar.

⚠️ Limitações conhecidas
Só observa. Não bloqueia, não isola equipamentos e não executa ações automáticas.
Não vê o conteúdo do tráfego criptografado. Trabalha com metadados, não com o que trafega dentro do HTTPS, por exemplo.
Rotina não é prova de legitimidade. Tráfego comum do próprio equipamento (como HTTPS, DNS e sincronização de horário) é tratado como rotina e não vai para a IA. Isso reduz o ruído, mas não garante que aquele tráfego seja legítimo.
Detecção de varredura básica. Baseada em uma janela de tempo curta; varreduras lentas podem passar despercebidas.
Alcance limitado à interface. Ele observa o que chega à interface em que está rodando. Em uma rede com switch comum, o tráfego entre outros equipamentos pode não ser visível.

A IA é uma segunda opinião. Modelos pequenos podem errar ou demorar. A decisão é sempre humana.
🗺️ Próximos passos
Alertas mais claros, com sugestão do que conferir primeiro.
Redução de falsos positivos.
Exportação dos registros para outras ferramentas.
Mais testes em redes e equipamentos diferentes.

🤝 Filosofia
O HÉRCULES é um parceiro do profissional, não um substituto. Seu propósito é ajudar a organizar as informações e a triar eventos, mantendo a interpretação e as decisões de segurança sob responsabilidade humana. Não substitui analisadores de pacotes, firewalls, antivírus, EDR ou profissionais de segurança.

🚧 Projeto em desenvolvimento.
