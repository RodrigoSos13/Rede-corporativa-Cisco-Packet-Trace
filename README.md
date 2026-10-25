# Rede Corporativa no Cisco Packet Tracer

Projeto de uma rede corporativa dividida em cinco sub-redes, com segmentação por departamento e interligação por roteador. A topologia combina conexões cabeadas e sem fio e utiliza a rede base **10.0.0.0/16**.

## Objetivos

- Organizar a rede em cinco departamentos com necessidades diferentes de hosts.
- Distribuir os endereços IPv4 por meio de sub-redes de tamanhos variados (VLSM).
- Interligar os departamentos por meio de um roteador.
- Validar a comunicação entre as sub-redes com testes de `ping`.

## Departamentos

| Departamento | Demanda de hosts |
| --- | ---: |
| Diretoria | 10 |
| Administrativo | 25 |
| Engenharia | 50 |
| Suporte | 30 |
| Laboratório | 60 |
| **Total** | **175** |

## Topologia

A rede possui um switch central conectado ao roteador e aos equipamentos de distribuição dos departamentos. Os switches locais conectam computadores e notebooks. A Engenharia e a Diretoria também possuem pontos de acesso para dispositivos sem fio.

O cenário utiliza dispositivos representativos de cada setor; a quantidade de equipamentos desenhados não corresponde necessariamente à demanda total de hosts.

## Plano de endereçamento

A divisão abaixo corresponde aos intervalos identificados na topologia:

| Departamento | Sub-rede | Máscara | Intervalo utilizável | Broadcast |
| --- | --- | --- | --- | --- |
| Laboratório | `10.0.0.0/26` | `255.255.255.192` | `10.0.0.1` a `10.0.0.62` | `10.0.0.63` |
| Engenharia | `10.0.0.64/26` | `255.255.255.192` | `10.0.0.65` a `10.0.0.126` | `10.0.0.127` |
| Suporte | `10.0.0.128/27` | `255.255.255.224` | `10.0.0.129` a `10.0.0.158` | `10.0.0.159` |
| Administrativo | `10.0.0.160/27` | `255.255.255.224` | `10.0.0.161` a `10.0.0.190` | `10.0.0.191` |
| Diretoria | `10.0.0.192/28` | `255.255.255.240` | `10.0.0.193` a `10.0.0.206` | `10.0.0.207` |

Os blocos `/26`, `/27` e `/28` oferecem, respectivamente, 62, 30 e 14 endereços utilizáveis. O endereço do gateway de cada departamento deve pertencer à sua sub-rede e ser consultado na configuração do roteador.

> A sub-rede do Suporte possui 30 endereços utilizáveis ao todo. Se a demanda for de 30 dispositivos finais mais o gateway, será necessário ampliar e reorganizar o endereçamento.

## Tecnologias e conceitos

- Cisco Packet Tracer.
- Endereçamento IPv4 e VLSM.
- Comutação Ethernet.
- Redes locais cabeadas e sem fio.
- Roteamento entre sub-redes.
- ICMP para testes de conectividade.

## Como abrir o projeto

1. Baixe o repositório pelo botão **Code → Download ZIP** ou clone-o com Git.
2. Extraia os arquivos, caso tenha baixado o ZIP.
3. Abra o Cisco Packet Tracer em uma versão compatível com o projeto.
4. Acesse **File → Open** e selecione `Rede_corp.pkt`.
5. Consulte a topologia e as configurações dos dispositivos.

## Testes de conectividade

Para testar a comunicação entre departamentos:

1. Selecione um computador e abra **Desktop → Command Prompt**.
2. Consulte o endereço IP, a máscara e o gateway com `ipconfig`.
3. Execute `ping` para o gateway do próprio departamento.
4. Execute `ping` para o IP de um dispositivo configurado em outro departamento:

```text
ping <IP_DO_DISPOSITIVO_DESTINO>
```

Repita os testes a partir de diferentes setores. Respostas ICMP recebidas indicam conectividade entre a origem e o destino testados. O modo **Simulation** permite acompanhar o percurso dos pacotes e investigar falhas.

## Arquivos do repositório

| Arquivo | Descrição |
| --- | --- |
| `Rede_corp.pkt` | Topologia e configurações da rede no Packet Tracer. |
| `README.md` | Documentação do projeto. |
