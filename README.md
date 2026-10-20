# Faturamento da Clínica

App desktop que uso no trabalho para fazer o faturamento mensal de uma clínica de reabilitação: emitir as notas fiscais, mandar para os planos de saúde e acompanhar quem pagou. Está na versão 2.3.1 e roda em mais de um PC da clínica.

> Código privado porque lida com dados de pacientes e da empresa. Aqui ficam o projeto, as decisões e o que aprendi.

## O problema
O faturamento era feito em planilhas e no portal da prefeitura, nota por nota. Para saber se um plano tinha pago, era preciso abrir nota por nota e cruzar com o extrato. Fácil esquecer paciente, mandar e-mail repetido ou deixar atraso passar.

## O que o app faz
- **Notas fiscais:** emite NFS-e uma a uma ou em lote (CSV) pela API da Focus NFe, com faixa colorida para separar produção de homologação (teste)
- **Envio de e-mails:** percorre mês > plano > paciente e envia as notas com anexos, com histórico e aviso de envio repetido
- **Conferência do mês:** cruza pacientes ativos × notas emitidas × e-mails enviados e mostra quem está faltando
- **Faturamento:** número de cada NFS-e, valor bruto e líquido, registro de pagamento e glosa, prazo por plano e alerta de atraso com regras por nível
- **Leitura de XML:** extrai número e valores direto do XML da nota (padrão nacional)
- **Cadastros:** pacientes, planos, terapias e configurações dentro do app, substituindo planilhas

## Stack
Python · Tkinter · API REST (Focus NFe) · XML · openpyxl · CSV/JSON · PyInstaller (gera o .exe)

## Números
- ~6 mil linhas de Python, organizadas em módulos (notas, e-mails, conferência, faturamento, cadastros)
- Distribuído como .exe para outros PCs, com dados separados do programa para atualizar sem perder nada

## O que aprendi
- Integrar com API de nota fiscal, tratando erros e reenvios automáticos
- Ler e interpretar XML fiscal
- Separar ambiente de teste (homologação) de produção, e testar antes de emitir de verdade
- Organizar um app grande em módulos e versionar mudanças com changelog
- Empacotar app Python como executável e atualizar sem perder os dados do usuário
