---
layout: post
title: "Como automatizei a instalação de pacotes no MGI"
date: 2026-03-09 10:00:00 -0300
---

Este é o meu primeiro artigo no blog. Aqui eu posso falar sobre como resolvi problemas de automação com Python.

## O problema
Nós tínhamos um parque tecnológico de 200 máquinas e precisávamos...

## A solução
O código abaixo em Shell Script foi o que resolveu o problema:

` ` `bash
sudo apt-get update && sudo apt-get upgrade -y
` ` `

*(Note que ali em cima, no Front Matter, passamos a variável `layout: post`. É isso que dirá ao Jekyll para usar a página que tem o **Giscus** no final!)*