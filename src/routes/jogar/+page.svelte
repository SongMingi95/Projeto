<script lang="ts">
    import { goto } from '$app/navigation';

   
    let teclado: string[][] = [
        ["A", "B", "C", "D", "E", "F", "G", "H", "I"],
        ["J", "K", "L", "M", "N", "O", "P", "Q", "R"],
        ["S", "T", "U", "V", "W", "X", "Y", "Z", "🎮"],
    ];

    
    let palavras: { palavra: string[], dica: string }[] = [
        { palavra: ["P", "A", "P", "A", "G", "A", "I", "O"], dica: "É uma ave." },
        { palavra: ["D", "E", "M", "O", "W", "E", "E", "K"], dica: "Evento do IFPE Campus Igarassu." },
        { palavra: ["P", "E", "R", "N", "A", "M", "B", "U", "C", "O"], dica: "É um estado." },
        { palavra: ["C", "A", "S", "A"], dica: "Local onde você mora." },
        { palavra: ["G", "A", "T", "O"], dica: "Animal felino que mia." },
        { palavra: ["P", "A", "I"], dica: "Figura paterna na família." },
        { palavra: ["S", "O", "L"], dica: "Estrela que ilumina o dia." },
        { palavra: ["L", "U", "A"], dica: "Satélite natural da Terra." },
        { palavra: ["C", "A", "C", "H", "O", "R", "R", "O"], dica: "Animal que late." },
        { palavra: ["B", "I", "C", "I", "C", "L", "E", "T", "A"], dica: "Meio de transporte com duas rodas." },
        { palavra: ["M", "A", "T", "E", "R", "I", "A", "L"], dica: "Substância usada para construir algo." },
        { palavra: ["E", "S", "C", "R", "I", "T", "O", "R"], dica: "Pessoa que escreve livros e artigos." },
        { palavra: ["P", "A", "L", "A", "V", "R", "A"], dica: "Unidade de comunicação." },
        { palavra: ["C", "A", "R", "R", "O"], dica: "Veículo usado para transporte de pessoas e cargas." },
        { palavra: ["R", "E", "L", "O", "G", "I", "O"], dica: "Instrumento usado para medir o tempo." },
        { palavra: ["E", "L", "E", "F", "A", "N", "T", "E"], dica: "Animal grande com tromba." },
        { palavra: ["T", "E", "L", "E", "F", "O", "N", "E"], dica: "Dispositivo para fazer chamadas e enviar mensagens." },
        { palavra: ["R", "A", "T", "O"], dica: "Pequeno roedor que pode ser encontrado em muitos lugares." },
        { palavra: ["M", "U", "S", "I", "C", "A"], dica: "Forma de arte que usa sons e ritmos." },
        { palavra: ["S", "O", "L", "D", "A", "D", "O"], dica: "Pessoa que serve em forças armadas." }
       
    ];

    
    let palavra: string[] = []; 
    let dica: string = "";
    let estado: string = "";
    let letrasErradas: Set<string> = new Set();
    let letrasUsadas: Set<string> = new Set();

    function escolherPalavraAleatoria(): void {
        
        const indiceAleatorio = Math.floor(Math.random() * palavras.length);
        const palavraEscolhida = palavras[indiceAleatorio];
        
        palavra = palavraEscolhida.palavra;
        dica = palavraEscolhida.dica;
        estado = "_".repeat(palavra.length);
        letrasErradas.clear();
        letrasUsadas.clear();
    }

    function clicou(letra: string): void {
        if (letrasUsadas.has(letra)) {
            alert('Você já tentou essa letra!');
            return;
        }

        letrasUsadas.add(letra);

        if (estado.indexOf('_') === -1) {
            return;
        }

        let e: string = "";
        let acertou = false;

        for (let i = 0; i < palavra.length; i++) {
            if (estado[i] === '_') {
                if (letra === palavra[i]) {
                    e += letra;
                    acertou = true;
                } else {
                    e += estado[i];
                }
            } else {
                e += estado[i];
            }
        }

        if (!acertou) {
            letrasErradas.add(letra);
            alert('Letra errada');
        }

        estado = e;

        
        if (estado.indexOf('_') === -1) {
            setTimeout(() => {
                alert('Parabéns, você ganhou!');
                escolherPalavraAleatoria();
            }, 100);
        }
    }

    function trocarPalavra(): void {
        escolherPalavraAleatoria();
    }

   
    escolherPalavraAleatoria();
</script>

<h1>Escolha uma letra</h1>

<h3>Dica: {dica}</h3>
<h3>
    {#each estado.split('') as caractere}
        <span class="letra">{caractere}</span>
    {/each}
</h3>

<table>
    {#each teclado as linha}
        <tr>
            {#each linha as letra}
                <td 
                    class="celula personagem" 
                    on:click={() => letra === "🎮" ? trocarPalavra() : clicou(letra)}
                >
                    {letra}
                </td>
            {/each}
        </tr>
    {/each}    
</table>

<br />

<a class="menu" href="/">Voltar ao Menu</a>
