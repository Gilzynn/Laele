// Gera um número aleatório entre 1 e 100 para iniciar a sequência
const numeroInicial = Math.floor(Math.random() * 100) + 1;

// Inicializa a variável de progressão
let progressao = [numeroInicial];

// Gera os próximos 5 números na sequência
for (let i = 0; i < 5; i++) {
  progressao.push(progressao[progressao.length - 1] + 3); // Pode ajustar o passo conforme necessário
}

// Função para verificar se o número fornecido pelo jogador está correto
function verificaPalpite(palpite) {
  if (palpite === progressao[progressao.length - 1] + 3) {
    return "Parabéns! Você acertou o próximo número na sequência.";
  } else {
    return "Tente novamente. Você errou.";
  }
}

// Exemplo de uso
const palpiteDoJogador = 13; // Substitua pelo palpite real do jogador
console.log(verificaPalpite(palpiteDoJogador));
