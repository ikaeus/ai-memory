# Fenda: histórico de controle da IA

Registro do que a IA está fazendo, já fez e ainda falta no projeto do jogo
Fenda (projeto "Meu jogo"). Os arquivos do jogo não ficam neste repositório;
a fonte completa é o `fenda-godot/ANDAMENTO.md` da pasta do projeto. Aqui fica
só o resumo de controle, atualizado a cada passo.

Atualizado em 2026-10-20.

## Regras de trabalho

- Um passo por vez. O próximo só começa quando o Matheus diz que está
  satisfeito (ou manda seguir sem testar).
- Tudo do jogo é criado no editor próprio (fichas em texto `[tipo id]` +
  `campo = valor`, desenhos em pixels). Nada de modelos 3D prontos de fora.
- Mundo de cubos (voxel) feito à mão, sem geração procedural.
- Cada erro resolvido entra na lista abaixo com a solução, para não repetir a
  investigação.

## Linha do tempo

| Quando | O que | Estado |
|---|---|---|
| Antes de 2026-10-19 | Protótipo 1 (C++/raylib, em metros) | Pronto, não mexer |
| Antes de 2026-10-19 | Protótipo 2 (C++/raylib, em cubos) | Parado |
| 2026-10-19 03:55 | Bonecos low-poly gerados por código em Godot | Rejeitado pelo Matheus |
| 2026-10-19 04:10 | Pesquisa de motor (Hytale mod, Godot, raylib) | Decidido: Godot |
| 2026-10-19 04:40-10:00 | Editor, etapas 1 a 5 (fichas, parâmetros, mundo de terreno, assets, objetos e regiões) | Feito; etapas 1-4 aprovadas |
| 2026-10-19 10:19 | Volta aos cubos: plano de 10 passos, tudo feito no editor | Em andamento |
| 2026-10-19 10:40 | Passo 1: blocos + editor de pixels | Feito |
| 2026-10-19 11:10 | Passo 2: mundo de cubos, pincéis, Testar aqui (pulo 1, escalar 2) | Feito |
| 2026-10-19 11:30 | Passo 3: blueprints (bancada, selecionar e salvar, carimbar, espalhar) | Feito |
| 2026-10-19 14:10 | Passo 4: corpo humano de 35 peças com dedos e encaixes | Feito, aguardando ok |
| 2026-10-19 15:05 | 35 animações básicas (Entidades > Animações) | Feito, aguardando ok |
| 2026-10-19 15:30 | Passo 5: itens no corpo (modelo em cubinhos, encaixe por categoria, 2 mãos com IK) | Feito, aguardando ok |
| 2026-10-19 19:55 | Servidor: um exe com editor/servidor/jogo, ambientes teste e oficial, publicar e promover versão | Feito |
| 2026-10-20 00:28 | Zip do projeto inteiro para baixar | Entregue |

## Fazendo agora

- Aguardando o ok do Matheus nos passos 4, 5 e nas animações.
- Envio ao PC pendente: exe novo em 5 partes e o conteúdo novo dos passos 1 a 5
  (sem sobrescrever fichas que ele criou lá e sem mandar o mundo antigo).

## Falta

Passos do plano dos cubos:

- 5b. Editor de entidades: jogador e monstros, editor de quadros-chave das
  animações, hitbox automática.
- 6. Partículas (editor de efeitos com prévia).
- 7. Cores e visual do jogo em fichas (paletas, luz, céu, contorno).
- 8. HUD editável, estilo Hades / Expedition 33.
- 9. Receitas, minérios, NPCs, lojas, missões.
- 10. Criador de magias com grade.

Também ficou para depois: roupas (peitoral, luva, calça, bota) sobre o corpo,
exe só do jogo (sem editor), servidor Linux, inventário e combate no servidor,
mundo em várias regiões.

## Erros resolvidos

- Editor não abria no PC: o envio aceita no máximo 25 MB por arquivo e uma
  parte do exe faltou. Solução: exe em 5 partes (`split -b 23500000`) e um .bat
  que junta tudo; depois do envio, conferir o tamanho do exe.
- O .bat antigo apagava as partes mesmo quando a cópia falhava com o editor
  aberto. Solução: o .bat novo recusa juntar com o editor aberto e só apaga as
  partes depois de trocar o exe.
- Envio ao PC podia apagar fichas criadas por ele. Solução: mandar só arquivos
  novos e a estrutura, conferindo a data de cada arquivo antes de gravar.
- Mão esquerda do corpo virava "mao_eireita" ao espelhar: trocar
  direita/esquerda primeiro e `_d`/`_e` só no fim; giro espelhado = (x, -y, -z).
- IK de duas mãos não alcançava o cabo: faltava a pose de segurar no braço
  principal e o IK rodava fora da árvore de cena.
- Bancada de blueprints com blocos trocados: copiar a paleta do mundo antes de
  criar o chão.
- Neblina lavava a imagem: usar neblina por profundidade (começo e fim).
- Servidor com porta ocupada falhava ao criar a rede: ele avisa e fecha sozinho.
- GDScript: `:=` não infere tipo vindo de dicionário ou `get_child()`; declarar
  o tipo. Script com erro em `godot -s` trava calado: mandar a saída para
  arquivo e usar `timeout`.
- Luz de desenho deixava morros sem lado escuro: usar 3 tons em vez de 2.
- Rosto e cabelo de personagem feitos só com formas em código não chegam ao
  visual que ele quer: não insistir nesse caminho.
