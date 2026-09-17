<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>Simulado Transpetro - Dutos e Terminais</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- MathJax para exibição de fórmulas -->
  <script>
    window.MathJax = {
      tex: { inlineMath: [['$', '$'], ['\\(', '\\)']] },
      svg: { fontCache: 'global' }
    };
  </script>
  <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" />
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap');
    body { 
      font-family: 'Plus Jakarta Sans', sans-serif; 
      -webkit-tap-highlight-color: transparent;
    }
    .custom-scroll::-webkit-scrollbar { width: 4px; height: 4px; }
    .custom-scroll::-webkit-scrollbar-track { background: #f1f5f9; }
    .custom-scroll::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
    .no-scrollbar::-webkit-scrollbar { display: none; }
    .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
  </style>
</head>
<body class="bg-slate-100 text-slate-800 min-h-screen flex flex-col antialiased">

  <!-- CABEÇALHO SUPERIOR COMPACTO -->
  <header class="bg-slate-900 text-white shadow-md sticky top-0 z-50 border-b border-slate-800">
    <div class="max-w-7xl mx-auto px-3 sm:px-4 py-2.5 flex items-center justify-between gap-2">
      
      <!-- Identificação do Concurso -->
      <div class="flex items-center space-x-2.5 min-w-0">
        <div class="w-9 h-9 sm:w-10 sm:h-10 shrink-0 rounded-xl bg-gradient-to-tr from-emerald-500 to-teal-400 flex items-center justify-center text-slate-950 font-extrabold text-lg shadow-sm">
          <i class="fa-solid fa-gas-pump text-sm sm:text-base"></i>
        </div>
        <div class="truncate">
          <div class="flex items-center gap-1.5">
            <h1 class="text-xs sm:text-base font-bold tracking-tight truncate">TRANSPETRO • SIMULADO</h1>
            <span class="bg-emerald-500/20 text-emerald-300 text-[9px] font-bold px-1.5 py-0.5 rounded border border-emerald-500/30 uppercase shrink-0">CESGRANRIO</span>
          </div>
          <p class="text-[10px] sm:text-xs text-slate-400 truncate">Dutos e Terminais (Nível Técnico)</p>
        </div>
      </div>

      <!-- Cronômetro & Acertos -->
      <div class="flex items-center gap-1.5 sm:gap-3 shrink-0">
        <div class="bg-slate-800 px-2 sm:px-3 py-1 sm:py-1.5 rounded-lg border border-slate-700 flex items-center gap-1.5 text-[11px] sm:text-xs">
          <i class="fa-regular fa-clock text-amber-400"></i>
          <span id="timer-display" class="font-mono font-bold text-slate-200">00:00:00</span>
          <button onclick="toggleTimer()" id="timer-btn" title="Pausar/Retomar" class="text-slate-400 hover:text-white ml-0.5">
            <i class="fa-solid fa-pause"></i>
          </button>
        </div>

        <div class="bg-emerald-950/70 px-2 sm:px-3 py-1 sm:py-1.5 rounded-lg border border-emerald-500/30 flex items-center gap-1.5 text-[11px] sm:text-xs">
          <i class="fa-solid fa-circle-check text-emerald-400"></i>
          <span id="top-accuracy-badge" class="text-emerald-300 font-bold">0%</span>
        </div>
      </div>

    </div>

    <!-- BARRA DESLIZANTE DE MATÉRIAS E NAVEGAÇÃO -->
    <div class="bg-slate-950 border-t border-slate-800/80 px-3 sm:px-4 py-2 overflow-x-auto no-scrollbar">
      <div class="max-w-7xl mx-auto flex items-center justify-between gap-3 min-w-max">
        
        <!-- Filtros por Matéria -->
        <div class="flex items-center gap-1.5 sm:gap-2">
          <button onclick="setSubjectFilter('TODAS')" id="btn-mat-todas" class="subject-btn px-2.5 sm:px-3 py-1 rounded-lg text-[11px] sm:text-xs font-bold transition flex items-center gap-1.5 bg-emerald-600 text-white shadow-sm ring-2 ring-emerald-400">
            <i class="fa-solid fa-layer-group"></i> Todas <span id="count-todas" class="ml-1 px-1.5 py-0.2 bg-black/25 rounded text-[10px]">20</span>
          </button>
          <button onclick="setSubjectFilter('Português')" id="btn-mat-port" class="subject-btn px-2.5 sm:px-3 py-1 rounded-lg text-[11px] sm:text-xs font-bold transition flex items-center gap-1.5 bg-slate-800 text-slate-300 border border-slate-700">
            <i class="fa-solid fa-book-open text-sky-400"></i> Português <span id="count-port" class="ml-1 px-1.5 py-0.2 bg-slate-900 rounded text-[10px]">5</span>
          </button>
          <button onclick="setSubjectFilter('Matemática')" id="btn-mat-mat" class="subject-btn px-2.5 sm:px-3 py-1 rounded-lg text-[11px] sm:text-xs font-bold transition flex items-center gap-1.5 bg-slate-800 text-slate-300 border border-slate-700">
            <i class="fa-solid fa-square-root-variable text-amber-400"></i> Matemática <span id="count-mat" class="ml-1 px-1.5 py-0.2 bg-slate-900 rounded text-[10px]">8</span>
          </button>
          <button onclick="setSubjectFilter('Dutos e Terminais')" id="btn-mat-dutos" class="subject-btn px-2.5 sm:px-3 py-1 rounded-lg text-[11px] sm:text-xs font-bold transition flex items-center gap-1.5 bg-slate-800 text-slate-300 border border-slate-700">
            <i class="fa-solid fa-gears text-purple-400"></i> Dutos & Terminais <span id="count-dutos" class="ml-1 px-1.5 py-0.2 bg-slate-900 rounded text-[10px]">7</span>
          </button>
        </div>

        <!-- Abas do Sistema -->
        <div class="flex items-center gap-1 border-l border-slate-800 pl-2">
          <button onclick="switchView('simulado')" id="view-tab-simulado" class="px-2.5 py-1 rounded-md text-[11px] sm:text-xs font-semibold bg-slate-800 text-emerald-400 border border-emerald-500/30">
            <i class="fa-solid fa-pen-to-square mr-1"></i> Questões
          </button>
          <button onclick="switchView('formulas')" id="view-tab-formulas" class="px-2.5 py-1 rounded-md text-[11px] sm:text-xs font-semibold text-slate-400 hover:text-white">
            <i class="fa-solid fa-lightbulb mr-1"></i> Resumos
          </button>
          <button onclick="switchView('desempenho')" id="view-tab-desempenho" class="px-2.5 py-1 rounded-md text-[11px] sm:text-xs font-semibold text-slate-400 hover:text-white">
            <i class="fa-solid fa-chart-simple mr-1"></i> Estatísticas
          </button>
        </div>

      </div>
    </div>
  </header>

  <!-- ÁREA DE CONTEÚDO PRINCIPAL -->
  <main class="max-w-7xl mx-auto px-3 sm:px-4 py-4 sm:py-6 flex-1 w-full">

    <!-- VIEW 1: SIMULADO DE QUESTÕES -->
    <div id="container-simulado" class="flex flex-col lg:grid lg:grid-cols-12 gap-4 sm:gap-6">

      <!-- COLUNA PRINCIPAL DA QUESTÃO (PRIORIDADE MOBILE: APARECE PRIMEIRO) -->
      <section class="order-1 lg:order-2 lg:col-span-8">
        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-4 sm:p-6 md:p-8 flex flex-col justify-between min-h-[520px]">
          
          <div>
            <!-- Cabeçalho da Questão -->
            <div class="flex flex-wrap items-center justify-between gap-2 pb-3 mb-3 border-b border-slate-100">
              <div class="flex items-center gap-1.5 sm:gap-2">
                <span id="card-q-number" class="text-xs font-extrabold px-2.5 py-1 rounded-lg bg-slate-900 text-white">Questão 1</span>
                <span id="card-q-subject" class="text-xs font-bold px-2.5 py-1 rounded-lg bg-sky-100 text-sky-900 border border-sky-200">Português</span>
                <span id="card-q-topic" class="text-xs px-2 py-1 rounded-lg bg-slate-100 text-slate-600 font-semibold hidden md:inline">Tópico</span>
              </div>
              
              <div class="flex items-center gap-1.5">
                <!-- Botão Dica -->
                <button onclick="toggleHint()" id="btn-toggle-hint" class="px-2.5 py-1 text-xs font-semibold rounded-lg bg-amber-50 text-amber-800 border border-amber-200 hover:bg-amber-100 transition flex items-center gap-1">
                  <i class="fa-regular fa-lightbulb"></i> <span id="hint-label">Dica</span>
                </button>
                <!-- Botão Mobile para Abrir Grade de Navegação -->
                <button onclick="toggleMobileNav()" class="lg:hidden px-2.5 py-1 text-xs font-semibold rounded-lg bg-slate-100 text-slate-700 border border-slate-200 hover:bg-slate-200 transition flex items-center gap-1">
                  <i class="fa-solid fa-table-cells"></i> <span id="mobile-nav-toggle-text">Ver Grade</span>
                </button>
              </div>
            </div>

            <!-- Caixa de Dica -->
            <div id="box-hint" class="hidden mb-4 p-3 sm:p-3.5 bg-amber-50 border border-amber-200 rounded-xl text-xs text-amber-950 flex items-start gap-2">
              <i class="fa-solid fa-lightbulb text-amber-600 mt-0.5 text-sm shrink-0"></i>
              <div id="content-hint" class="leading-relaxed"></div>
            </div>

            <!-- Contexto / Texto de Apoio -->
            <div id="box-context" class="hidden mb-4 p-3.5 sm:p-4 bg-slate-50 border border-slate-200 rounded-xl text-xs text-slate-700 leading-relaxed max-h-48 overflow-y-auto custom-scroll">
              <div class="font-bold text-slate-900 mb-1 flex items-center gap-1.5">
                <i class="fa-solid fa-align-left text-slate-400"></i> Texto / Contexto:
              </div>
              <div id="content-context"></div>
            </div>

            <!-- Enunciado Principal -->
            <div id="content-statement" class="text-slate-900 font-semibold text-sm sm:text-base leading-relaxed mb-5 overflow-x-auto">
              <!-- Injetado via JS -->
            </div>

            <!-- Lista de Alternativas -->
            <div id="container-options" class="space-y-2.5 sm:space-y-3">
              <!-- Botões de alternativas -->
            </div>

            <!-- Resolução Comentada -->
            <div id="box-rationale" class="hidden mt-5 p-4 sm:p-5 rounded-xl border text-xs sm:text-sm leading-relaxed transition-all">
              <!-- Injetado via JS -->
            </div>
          </div>

          <!-- Rodapé de Navegação com Botões Grandes de Fácil Toque -->
          <div class="mt-6 pt-4 border-t border-slate-100 flex items-center justify-between gap-2">
            <button onclick="navigateQuestion(-1)" id="btn-prev-question" class="flex-1 sm:flex-none justify-center px-4 py-2.5 rounded-xl border border-slate-200 active:bg-slate-100 text-slate-700 text-xs sm:text-sm font-semibold flex items-center gap-2 transition">
              <i class="fa-solid fa-arrow-left"></i> Anterior
            </button>
            
            <div class="text-[11px] sm:text-xs font-semibold text-slate-500 text-center px-2">
              <span id="footer-index-display" class="text-slate-900 font-bold">1</span> de <span id="footer-total-display">20</span>
            </div>

            <button onclick="navigateQuestion(1)" id="btn-next-question" class="flex-1 sm:flex-none justify-center px-4 py-2.5 rounded-xl bg-emerald-600 active:bg-emerald-700 text-white text-xs sm:text-sm font-bold flex items-center gap-2 shadow-sm transition">
              Próxima <i class="fa-solid fa-arrow-right"></i>
            </button>
          </div>

        </div>
      </section>

      <!-- COLUNA LATERAL: GABARITO VISUAL E APROVEITAMENTO (NO CELULAR VEM DEPOIS OU FICA OCULTA ATÉ CLICAR) -->
      <aside id="sidebar-nav" class="order-2 lg:order-1 lg:col-span-4 space-y-4 hidden lg:block">
        
        <!-- Cartão da Grade de Navegação -->
        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-4">
          <div class="flex items-center justify-between mb-2.5">
            <div>
              <span class="text-[9px] font-bold uppercase tracking-wider text-slate-400">Navegação</span>
              <h2 id="badge-current-subject" class="text-xs sm:text-sm font-bold text-slate-900 truncate">
                Todas as Matérias
              </h2>
            </div>
            <span id="filtered-progress-tag" class="text-xs font-bold px-2 py-0.5 rounded bg-slate-100 text-slate-700">1 / 20</span>
          </div>

          <!-- Grade de Botões (1 a 20) -->
          <div id="grid-buttons" class="grid grid-cols-5 gap-1.5 max-h-56 overflow-y-auto pr-1 custom-scroll py-1">
            <!-- Gerado via JS -->
          </div>

          <!-- Legenda -->
          <div class="mt-3 pt-2.5 border-t border-slate-100 grid grid-cols-3 gap-1 text-[10px] text-slate-500 text-center font-medium">
            <span class="flex items-center justify-center gap-1"><span class="w-2 h-2 rounded bg-emerald-500"></span> Correta</span>
            <span class="flex items-center justify-center gap-1"><span class="w-2 h-2 rounded bg-rose-500"></span> Errada</span>
            <span class="flex items-center justify-center gap-1"><span class="w-2 h-2 rounded bg-slate-200"></span> Pendente</span>
          </div>
        </div>

        <!-- Aproveitamento por Matéria -->
        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-4 space-y-3">
          <h3 class="text-xs font-bold text-slate-800 uppercase tracking-wider flex items-center justify-between">
            <span>Aproveitamento por Bloco</span>
            <i class="fa-solid fa-chart-line text-emerald-600"></i>
          </h3>
          
          <!-- Português -->
          <div class="space-y-1">
            <div class="flex justify-between text-xs">
              <span class="font-medium text-slate-700 flex items-center gap-1.5"><i class="fa-solid fa-book-open text-sky-500 text-[10px]"></i> Português:</span>
              <span id="score-port" class="font-bold text-slate-800">0/5 (0%)</span>
            </div>
            <div class="w-full bg-slate-100 rounded-full h-2 overflow-hidden">
              <div id="bar-port" class="bg-sky-500 h-2 rounded-full transition-all duration-300" style="width: 0%"></div>
            </div>
          </div>

          <!-- Matemática -->
          <div class="space-y-1">
            <div class="flex justify-between text-xs">
              <span class="font-medium text-slate-700 flex items-center gap-1.5"><i class="fa-solid fa-square-root-variable text-amber-500 text-[10px]"></i> Matemática:</span>
              <span id="score-mat" class="font-bold text-slate-800">0/8 (0%)</span>
            </div>
            <div class="w-full bg-slate-100 rounded-full h-2 overflow-hidden">
              <div id="bar-mat" class="bg-amber-500 h-2 rounded-full transition-all duration-300" style="width: 0%"></div>
            </div>
          </div>

          <!-- Dutos & Terminais -->
          <div class="space-y-1">
            <div class="flex justify-between text-xs">
              <span class="font-medium text-slate-700 flex items-center gap-1.5"><i class="fa-solid fa-gears text-purple-500 text-[10px]"></i> Dutos:</span>
              <span id="score-dutos" class="font-bold text-slate-800">0/7 (0%)</span>
            </div>
            <div class="w-full bg-slate-100 rounded-full h-2 overflow-hidden">
              <div id="bar-dutos" class="bg-purple-600 h-2 rounded-full transition-all duration-300" style="width: 0%"></div>
            </div>
          </div>

          <button onclick="resetAnswers()" class="w-full mt-2 py-2 text-xs font-semibold text-rose-600 hover:bg-rose-50 border border-rose-200 rounded-xl transition flex items-center justify-center gap-1.5">
            <i class="fa-solid fa-rotate-left"></i> Limpar Respostas
          </button>
        </div>

      </aside>

    </div>

    <!-- VIEW 2: RESUMOS E MACETES -->
    <div id="container-formulas" class="hidden space-y-4 sm:space-y-6">
      <div class="bg-gradient-to-r from-slate-900 to-slate-800 text-white rounded-2xl p-4 sm:p-6 shadow-sm flex flex-col md:flex-row md:items-center justify-between gap-3">
        <div>
          <span class="text-xs font-bold text-emerald-400 uppercase tracking-wider">Revisão Rápida</span>
          <h2 class="text-base sm:text-xl font-bold mt-0.5">Fórmulas e Regras Chave</h2>
          <p class="text-xs text-slate-300 mt-0.5">Matemática, Mecânica dos Fluidos e Dutos.</p>
        </div>
        <div class="flex flex-wrap gap-1.5">
          <button onclick="filterFlashcards('TODOS')" class="px-2.5 py-1 bg-slate-700 text-white hover:bg-slate-600 rounded-lg text-xs font-bold transition">Todos</button>
          <button onclick="filterFlashcards('Matemática')" class="px-2.5 py-1 bg-amber-500/20 text-amber-300 hover:bg-amber-500/30 rounded-lg text-xs font-bold border border-amber-400/30 transition">Matemática</button>
          <button onclick="filterFlashcards('Fluidos/Dutos')" class="px-2.5 py-1 bg-purple-500/20 text-purple-300 hover:bg-purple-500/30 rounded-lg text-xs font-bold border border-purple-400/30 transition">Dutos</button>
        </div>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-3 sm:gap-4" id="flashcards-grid">
        <!-- Injetado por JS -->
      </div>
    </div>

    <!-- VIEW 3: DESEMPENHO E ESTATÍSTICAS -->
    <div id="container-desempenho" class="hidden space-y-4 sm:space-y-6">
      <div class="grid grid-cols-1 sm:grid-cols-3 gap-3 sm:gap-4">
        <div class="bg-white p-4 sm:p-6 rounded-2xl border border-slate-200 shadow-sm text-center">
          <span class="text-xs font-bold uppercase tracking-wider text-slate-400">Aproveitamento Geral</span>
          <div id="stat-total-percent" class="text-3xl sm:text-4xl font-extrabold text-emerald-600 my-1 sm:my-2">0%</div>
          <p class="text-xs text-slate-500" id="stat-total-detail">0 acertos de 0 resolvidas</p>
        </div>
        <div class="bg-white p-4 sm:p-6 rounded-2xl border border-slate-200 shadow-sm text-center">
          <span class="text-xs font-bold uppercase tracking-wider text-slate-400">Respondidas</span>
          <div id="stat-answered-count" class="text-3xl sm:text-4xl font-extrabold text-slate-900 my-1 sm:my-2">0 / 20</div>
          <p class="text-xs text-slate-500">Restam <span id="stat-remaining-count">20</span> questões</p>
        </div>
        <div class="bg-white p-4 sm:p-6 rounded-2xl border border-slate-200 shadow-sm text-center">
          <span class="text-xs font-bold uppercase tracking-wider text-slate-400">Pontuação Estimada</span>
          <div id="stat-points" class="text-3xl sm:text-4xl font-extrabold text-teal-600 my-1 sm:my-2">0.0 pts</div>
          <p class="text-xs text-slate-500">1,0 pt por acerto</p>
        </div>
      </div>

      <div class="bg-white rounded-2xl p-4 sm:p-6 border border-slate-200 shadow-sm">
        <h3 class="text-sm font-bold text-slate-900 mb-3 flex items-center gap-2">
          <i class="fa-solid fa-bullseye text-emerald-600"></i> Desempenho por Matéria
        </h3>
        <div id="stats-subject-bars" class="space-y-3">
          <!-- Injetado por JS -->
        </div>
      </div>
    </div>

  </main>

  <footer class="bg-white border-t border-slate-200 py-3 text-center text-[11px] text-slate-500">
    Simulado Oficial Transpetro • Técnico de Dutos e Terminais
  </footer>

  <!-- SCRIPT COM BANCO DE DADOS COMPLETO E SUPORTE A TOUCH -->
  <script>
    const questionsDatabase = [
      // ================= LÍNGUA PORTUGUESA (1 A 5) =================
      {
        id: 1,
        sourceNumber: 1,
        subject: "Português",
        topic: "Compreensão e Tese Central",
        context: "Texto: 'Brasil, paraíso dos agrotóxicos' - Debate o conflito entre o modelo agrícola intensivo em pesticidas versus a viabilidade da agricultura agroecológica familiar.",
        statement: "De acordo com as ideias desenvolvidas no texto, o objetivo principal do autor é discutir a:",
        options: [
          { letter: "A", text: "contraposição entre a agricultura orgânica e a convencional, baseada no uso de agrotóxicos.", correct: true },
          { letter: "B", text: "implementação de monoculturas para a renovação do bem-sucedido modelo agrário brasileiro.", correct: false },
          { letter: "C", text: "importância de o nosso país se manter na liderança na concorrência mundial do agronegócio.", correct: false },
          { letter: "D", text: "intoxicação dos trabalhadores e a contaminação ambiental provocados pela agricultura familiar.", correct: false },
          { letter: "E", text: "perspectiva de o agronegócio conseguir produzir alimentos para uma população de sete bilhões de pessoas.", correct: false }
        ],
        hint: "Observe o contraponto feito em todo o texto entre os danos do modelo químico tradicional e as propostas agroecológicas alternativas.",
        rationale: "Gabarito: <strong>A</strong>. O texto contrapõe os dois modelos produtivos: a monocultura convencional (grande usuária de venenos agrícolas) e a agricultura agroecológica orgânica, demonstrando a viabilidade desta última."
      },
      {
        id: 2,
        sourceNumber: 2,
        subject: "Português",
        topic: "Identificação da Proposta de Solução",
        context: "Parágrafo 7: 'Precisamos de outra estrutura agrária – baseada em propriedades menores, com produção diversificada, privilegiando mercados locais...'",
        statement: "O trecho que apresenta explicitamente a proposta do autor para a solução do problema discutido é:",
        options: [
          { letter: "A", text: "\"O Brasil vive um drama: ao acordar do sonho de uma economia agrária pujante, o país desperta para o pesadelo de ser... o maior consumidor de agrotóxicos...\"", correct: false },
          { letter: "B", text: "\"A Bolsa de Chicago define o preço da soja; mas não considera que, para se produzir cada saca, são aplicadas generosas doses de agrotóxicos...\"", correct: false },
          { letter: "C", text: "\"Levando-se em conta os casos crônicos, acrescidos da contaminação ambiental difusa nos ecossistemas, os prejuízos podem atingir cifras assustadoramente maiores.\"", correct: false },
          { letter: "D", text: "\"Todos os milhares de profissionais envolvidos no comércio e na manipulação dessas substâncias são potenciais vítimas.\"", correct: false },
          { letter: "E", text: "\"Precisamos de outra estrutura agrária – baseada em propriedades menores, com produção diversificada, privilegiando mercados locais e contemplando a conservação da biodiversidade.\"", correct: true }
        ],
        hint: "Identifique o trecho prescritivo que começa com 'Precisamos de...', onde o autor prescreve a mudança necessária.",
        rationale: "Gabarito: <strong>E</strong>. É o único trecho propositivo do texto, indicando as diretrizes para superar o modelo nocivo de produção."
      },
      {
        id: 3,
        sourceNumber: 3,
        subject: "Português",
        topic: "Semântica e Externalidades Negativas",
        context: "Parágrafo 2: '...garante que as \"externalidades negativas\" de nosso modelo agrário continuam de fora dos cálculos.'",
        statement: "No trecho citado, a expressão técnica 'externalidades negativas' refere-se diretamente aos:",
        options: [
          { letter: "A", text: "prejuízos sociais e ambientais causados pelo uso dos agrotóxicos.", correct: true },
          { letter: "B", text: "opiniões dos produtores sobre os benefícios dos defensivos agrícolas.", correct: false },
          { letter: "C", text: "lucros obtidos com o grande crescimento das exportações do agronegócio.", correct: false },
          { letter: "D", text: "efeitos das flutuações das commodities na balança comercial.", correct: false },
          { letter: "E", text: "gastos financeiros diretos com adubos químicos importados.", correct: false }
        ],
        hint: "Na teoria econômica, externalidade negativa é o dano imposto a terceiros (sociedade e meio ambiente) não contabilizado no preço de venda.",
        rationale: "Gabarito: <strong>A</strong>. O autor explica que os custos com saúde pública e contaminação ecológica gerados pelos pesticidas recaem sobre a sociedade, ficando de fora da precificação da saca de soja."
      },
      {
        id: 4,
        sourceNumber: 5,
        subject: "Português",
        topic: "Sinonímia e Vocabulário",
        context: "'...ao acordar do sonho de uma economia agrária pujante, o país desperta para o pesadelo de ser o maior consumidor de veneno...'",
        statement: "No trecho em destaque, a palavra 'pujante' pode ser substituída sem prejuízo de sentido por:",
        options: [
          { letter: "A", text: "apreciada", correct: false },
          { letter: "B", text: "incipiente", correct: false },
          { letter: "C", text: "inoperante", correct: false },
          { letter: "D", text: "possante", correct: true },
          { letter: "E", text: "moderna", correct: false }
        ],
        hint: "'Pujante' expressa força vigorosa, robustez e grande potência de crescimento.",
        rationale: "Gabarito: <strong>D</strong>. Pujante é sinônimo direto de robusta, possante, vigorosa e forte."
      },
      {
        id: 5,
        sourceNumber: 8,
        subject: "Português",
        topic: "Emprego do Acento Grave (Crase)",
        statement: "O acento grave indicativo de crase está empregado rigorosamente de acordo com a norma-padrão em:",
        options: [
          { letter: "A", text: "A água consumida pela população apresenta resíduos, o que prejudica a vida de todos que à ingerem, por estar contaminada.", correct: false },
          { letter: "B", text: "A produção de alimentos orgânicos representa um avanço, pois beneficia à agricultura familiar do país.", correct: false },
          { letter: "C", text: "Os especialistas chegaram à conclusão de que os governos precisam tomar medidas urgentes contra os estragos.", correct: true },
          { letter: "D", text: "A preservação do meio ambiente se aplica à diversas situações que envolvem o bem-estar comunitário.", correct: false },
          { letter: "E", text: "Os produtores responsáveis pelas lavouras foram forçados à adotar novos critérios operacionais.", correct: false }
        ],
        hint: "Lembre-se: não há crase antes de verbo ('adotar'), pronome oblíquo ('ingerem'), nem com 'a' no singular diante de palavra no plural ('à diversas').",
        rationale: "Gabarito: <strong>C</strong>. Quem chega, chega 'a' (preposição) + a conclusão (artigo feminino) = à conclusão."
      },

      // ================= MATEMÁTICA (QUESTÕES 11 A 18) =================
      {
        id: 6,
        sourceNumber: 11,
        subject: "Matemática",
        topic: "Potenciação e Comparação de Potências",
        statement: "Considerando-se os números reais $2^{75}$, $3^{50}$ e $4^{37}$, o menor e o maior deles são, respectivamente:",
        options: [
          { letter: "A", text: "$4^{37}$ e $3^{50}$", correct: true },
          { letter: "B", text: "$4^{37}$ e $2^{75}$", correct: false },
          { letter: "C", text: "$3^{50}$ e $2^{75}$", correct: false },
          { letter: "D", text: "$3^{50}$ e $4^{37}$", correct: false },
          { letter: "E", text: "$2^{75}$ e $4^{37}$", correct: false }
        ],
        hint: "Passe $4^{37}$ para a base 2: $4^{37} = (2^2)^{37} = 2^{74}$. Para comparar $2^{75}$ e $3^{50}$, use o expoente 25: $2^{75} = (2^3)^{25} = 8^{25}$ e $3^{50} = (3^2)^{25} = 9^{25}$.",
        rationale: "Gabarito: <strong>A</strong>.<br>1º) $4^{37} = (2^2)^{37} = 2^{74} < 2^{75}$.<br>2º) $2^{75} = 8^{25}$ e $3^{50} = 9^{25} \\implies 2^{75} < 3^{50}$.<br>Menor: $4^{37}$; Maior: $3^{50}$."
      },
      {
        id: 7,
        sourceNumber: 12,
        subject: "Matemática",
        topic: "Matemática Financeira",
        statement: "Um produto que custava R$ 200,00 sofreu dois aumentos sucessivos: o primeiro de 10% e o segundo de 20%. Em seguida, sobre o novo preço, foi concedido um desconto de 15%. O preço final desse produto passou a ser:",
        options: [
          { letter: "A", text: "R$ 224,40", correct: true },
          { letter: "B", text: "R$ 230,00", correct: false },
          { letter: "C", text: "R$ 237,60", correct: false },
          { letter: "D", text: "R$ 242,00", correct: false },
          { letter: "E", text: "R$ 215,00", correct: false }
        ],
        hint: "Utilize o produto dos fatores: $V_f = 200 \\times 1,10 \\times 1,20 \\times 0,85$.",
        rationale: "Gabarito: <strong>A</strong>.<br>$200 \\times 1,10 = 220$<br>$220 \\times 1,20 = 264$<br>$264 \\times 0,85 = \\text{R\\$ } 224,40$."
      },
      {
        id: 8,
        sourceNumber: 13,
        subject: "Matemática",
        topic: "Função Afim e Equação de Custos",
        context: "Uma transportadora que opera carretas-tanque cobra uma taxa fixa de R$ 150,00 mais R$ 4,50 por quilômetro rodado no transporte de derivados de petróleo.",
        statement: "Se um cliente pagou o valor total de R$ 960,00 por um frete, a distância percorrida pela carreta-tanque foi de:",
        options: [
          { letter: "A", text: "160 km", correct: false },
          { letter: "B", text: "175 km", correct: false },
          { letter: "C", text: "180 km", correct: true },
          { letter: "D", text: "190 km", correct: false },
          { letter: "E", text: "210 km", correct: false }
        ],
        hint: "Monte a equação linear: $150 + 4,50 \\cdot x = 960$. Isole $x$.",
        rationale: "Gabarito: <strong>C</strong>.<br>$4,50x = 960 - 150 = 810$<br>$x = \\frac{810}{4,50} = 180\\text{ km}$."
      },
      {
        id: 9,
        sourceNumber: 14,
        subject: "Matemática",
        topic: "Progressão Aritmética (PA)",
        statement: "Em uma tubulação industrial, o diâmetro nominal dos anéis metálicos cresce segundo uma progressão aritmética. Se o 3º anel mede 17 cm e o 7º anel mede 33 cm, qual é o diâmetro do 1º anel?",
        options: [
          { letter: "A", text: "9 cm", correct: true },
          { letter: "B", text: "10 cm", correct: false },
          { letter: "C", text: "11 cm", correct: false },
          { letter: "D", text: "12 cm", correct: false },
          { letter: "E", text: "13 cm", correct: false }
        ],
        hint: "$a_7 - a_3 = 4r$. Encontre $r$ e depois calcule $a_1 = a_3 - 2r$.",
        rationale: "Gabarito: <strong>A</strong>.<br>$33 - 17 = 4r \\implies 16 = 4r \\implies r = 4\\text{ cm}$.<br>$a_1 = 17 - 2(4) = 9\\text{ cm}$."
      },
      {
        id: 10,
        sourceNumber: 15,
        subject: "Matemática",
        topic: "Estatística (Desvio Padrão)",
        context: "Em uma escola, há 5 turmas com 60 alunos cada. As notas obtidas foram:\n• Turma 1: 30 notas 0 e 30 notas 10\n• Turma 2: 30 notas 2 e 30 notas 8\n• Turma 3: 30 notas 3 e 30 notas 7\n• Turma 4: 30 notas 4 e 30 notas 6\n• Turma 5: 60 notas iguais a 5.",
        statement: "Em qual das turmas o desvio-padrão das notas obtidas foi rigorosamente igual a zero?",
        options: [
          { letter: "A", text: "Turma 1", correct: false },
          { letter: "B", text: "Turma 2", correct: false },
          { letter: "C", text: "Turma 3", correct: false },
          { letter: "D", text: "Turma 4", correct: false },
          { letter: "E", text: "Turma 5", correct: true }
        ],
        hint: "O desvio-padrão mede a dispersão. Quando todos os valores são idênticos, a dispersão é nula.",
        rationale: "Gabarito: <strong>E</strong>. Na Turma 5, todos tiraram 5, portanto não há variação em relação à média (desvio padrão $\\sigma = 0$)."
      },
      {
        id: 11,
        sourceNumber: 16,
        subject: "Matemática",
        topic: "Cinemática e Proporcionalidade",
        statement: "Um veículo percorreu a distância entre dois pontos A e B com velocidade constante de $80\\text{ km/h}$. No retorno, com velocidade de $100\\text{ km/h}$, gastou 30 minutos a menos. Quanto tempo o carro levou na primeira viagem?",
        options: [
          { letter: "A", text: "3 h 00 min", correct: false },
          { letter: "B", text: "2 h 30 min", correct: true },
          { letter: "C", text: "2 h 00 min", correct: false },
          { letter: "D", text: "1 h 45 min", correct: false },
          { letter: "E", text: "1 h 30 min", correct: false }
        ],
        hint: "A distância é igual: $80 \\cdot t = 100 \\cdot (t - 0,5)$.",
        rationale: "Gabarito: <strong>B</strong>.<br>$80t = 100t - 50 \\implies 20t = 50 \\implies t = 2,5\\text{ h} = 2\\text{ horas e } 30\\text{ minutos}$."
      },
      {
        id: 12,
        sourceNumber: 17,
        subject: "Matemática",
        topic: "Regra de Três Composta / Bombas",
        statement: "Duas bombas idênticas de transferência conseguem bombear $600\\text{ m}^3$ de óleo combustível em 4 horas. Para descarregar $1.200\\text{ m}^3$ do mesmo produto em apenas 2 horas, quantas bombas idênticas serão necessárias?",
        options: [
          { letter: "A", text: "4", correct: false },
          { letter: "B", text: "6", correct: false },
          { letter: "C", text: "8", correct: true },
          { letter: "D", text: "10", correct: false },
          { letter: "E", text: "12", correct: false }
        ],
        hint: "Vazão por bomba: $\\frac{600}{2 \\times 4} = 75\\text{ m}^3/\\text{h}$. Vazão necessária: $\\frac{1.200}{2} = 600\\text{ m}^3/\\text{h}$.",
        rationale: "Gabarito: <strong>C</strong>.<br>Total de bombas necessárias: $\\frac{600}{75} = 8\\text{ bombas}$."
      },
      {
        id: 13,
        sourceNumber: 19,
        subject: "Matemática",
        topic: "Geometria Plana (Triângulo Retângulo)",
        context: "Em um triângulo retângulo ABC, o ângulo reto localiza-se no vértice A. O comprimento da hipotenusa BC é igual a 20 cm e o cateto AB mede 12 cm.",
        statement: "Qual é a área, em $\\text{cm}^2$, desse triângulo?",
        options: [
          { letter: "A", text: "16", correct: false },
          { letter: "B", text: "48", correct: false },
          { letter: "C", text: "60", correct: false },
          { letter: "D", text: "96", correct: true },
          { letter: "E", text: "192", correct: false }
        ],
        hint: "Por Pitágoras: $20^2 = 12^2 + AC^2 \\implies AC = 16\\text{ cm}$. Área = $\\frac{12 \\times 16}{2}$.",
        rationale: "Gabarito: <strong>D</strong>.<br>$AC = \\sqrt{400 - 144} = 16\\text{ cm}$.<br>Área: $\\frac{12 \\times 16}{2} = 96\\text{ cm}^2$."
      },

      // ================= DUTOS E TERMINAIS (14 A 20) =================
      {
        id: 14,
        sourceNumber: 26,
        subject: "Dutos e Terminais",
        topic: "Física Quântica / Efeito Fotoelétrico",
        statement: "O princípio fundamental do efeito fotoelétrico, essencial para dispositivos de automação e segurança ótica, consiste na:",
        options: [
          { letter: "A", text: "emissão de luz quando elétrons colidem com átomos metálicos.", correct: false },
          { letter: "B", text: "ejeção de elétrons de uma superfície condutora quando exposta a fótons com energia suficiente.", correct: true },
          { letter: "C", text: "reflexão total da luz em uma superfície metálica espelhada.", correct: false },
          { letter: "D", text: "geração de calor por refração total através de fluídos transparentes.", correct: false },
          { letter: "E", text: "ionização exclusiva por ondas de baixa frequência na faixa de rádio.", correct: false }
        ],
        hint: "A luz incidente arranca fotoelétrons da superfície quando a energia do fóton supera a função trabalho.",
        rationale: "Gabarito: <strong>B</strong>. O efeito fotoelétrico é a ejeção de elétrons por um condutor excitado por fótons de frequência superior à frequência de corte."
      },
      {
        id: 15,
        sourceNumber: 27,
        subject: "Dutos e Terminais",
        topic: "Petroquímica e Reações de Hidrocarbonetos",
        context: "Reações:\n1) $X + Cl_2 \\xrightarrow{UV} Y + HCl$\n2) $\\text{Benzeno} + Y \\xrightarrow{AlCl_3} \\text{Tolueno} + HCl$\n3) $\\text{Tolueno} + Z \\xrightarrow{H_2SO_4, 30^{\\circ}C} \\text{orto/para-nitrotolueno}$",
        statement: "Na síntese de derivados petroquímicos aromáticos, as substâncias X, Y e Z são, respectivamente:",
        options: [
          { letter: "A", text: "CH3Cl, CH4, HONO2", correct: false },
          { letter: "B", text: "CH3Cl, HONO2, CH4", correct: false },
          { letter: "C", text: "CH4, HONO2, CH3Cl", correct: false },
          { letter: "D", text: "CH4, CH3Cl, HONO2 (HNO3)", correct: true },
          { letter: "E", text: "HONO2, CH4, CH3Cl", correct: false }
        ],
        hint: "X é o metano ($CH_4$), Y é o cloreto de metila ($CH_3Cl$) e Z é o ácido nítrico ($HONO_2$).",
        rationale: "Gabarito: <strong>D</strong>. Cloração do metano forma $CH_3Cl$, que alquila o benzeno a tolueno, sofrendo nitração posterior com ácido nítrico."
      },
      {
        id: 16,
        sourceNumber: 28,
        subject: "Dutos e Terminais",
        topic: "Mecânica (MUV)",
        statement: "Um carrinho de movimentação de tubulações em um terminal parte do repouso e atinge a velocidade de $2,0\\text{ m/s}$ após 4 segundos em movimento uniformemente variado. A distância percorrida é de:",
        options: [
          { letter: "A", text: "2 metros", correct: false },
          { letter: "B", text: "4 metros", correct: true },
          { letter: "C", text: "6 metros", correct: false },
          { letter: "D", text: "8 metros", correct: false },
          { letter: "E", text: "10 metros", correct: false }
        ],
        hint: "$a = \\frac{\\Delta v}{\\Delta t} = \\frac{2}{4} = 0,5\\text{ m/s}^2$. Distância: $\\Delta S = \\frac{a \\cdot t^2}{2}$.",
        rationale: "Gabarito: <strong>B</strong>.<br>$\\Delta S = \\frac{0,5 \\times 4^2}{2} = \\frac{0,5 \\times 16}{2} = 4\\text{ metros}$."
      },
      {
        id: 17,
        sourceNumber: 30,
        subject: "Dutos e Terminais",
        topic: "Dinâmica em Rampa sem Atrito",
        statement: "No descarregamento de um lote de conexões de aço de massa $m$ por uma rampa inclinada de ângulo $\\alpha$, desprezando-se o atrito, a aceleração de descida da carga:",
        options: [
          { letter: "A", text: "é nula.", correct: false },
          { letter: "B", text: "é igual à gravidade g.", correct: false },
          { letter: "C", text: "independe do ângulo de inclinação.", correct: false },
          { letter: "D", text: "independe da massa da carga.", correct: true },
          { letter: "E", text: "é inversamente proporcional à gravidade.", correct: false }
        ],
        hint: "$F_{res} = m \\cdot g \\cdot \\text{sen}(\\alpha) = m \\cdot a \\implies a = g \\cdot \\text{sen}(\\alpha)$.",
        rationale: "Gabarito: <strong>D</strong>. Como a massa é cancelada na equação fundamental, a aceleração independe da massa da carga."
      },
      {
        id: 18,
        sourceNumber: 39,
        subject: "Dutos e Terminais",
        topic: "Instrumentação / Tubo de Venturi",
        context: "Tubo de Venturi instalado em linha de duto com estrangulamento da seção e tubos piezométricos verticais registrando desnível $\\Delta h$.",
        statement: "Nas instalações de transporte de hidrocarbonetos e derivados, o tubo de Venturi é o elemento primário utilizado para medir:",
        options: [
          { letter: "A", text: "calor latente", correct: false },
          { letter: "B", text: "temperatura termodinâmica", correct: false },
          { letter: "C", text: "potência térmica", correct: false },
          { letter: "D", text: "vazão de escoamento", correct: true },
          { letter: "E", text: "viscosidade cinemática", correct: false }
        ],
        hint: "O estrangulamento gera uma queda de pressão estática proporcional ao quadrado da velocidade (Bernoulli).",
        rationale: "Gabarito: <strong>D</strong>. O tubo de Venturi é o principal medidor deprimogênio de vazão em linhas industriais."
      },
      {
        id: 19,
        sourceNumber: 40,
        subject: "Dutos e Terminais",
        topic: "Mecânica dos Fluidos / Torricelli",
        context: "Tanque de terminal com nível de água na cota $h_1 = 10,8\\text{ m}$ e duto de saída circular de área $20\\text{ cm}^2$ localizado na cota $h_2 = 9\\text{ m}$. Dados: $\\rho = 1.000\\text{ kg/m}^3$, $g = 10\\text{ m/s}^2$.",
        statement: "A vazão mássica de água descarregada pelo bocal do tanque, em kg/s, é de:",
        options: [
          { letter: "A", text: "0,012", correct: false },
          { letter: "B", text: "0,12", correct: false },
          { letter: "C", text: "1,2", correct: false },
          { letter: "D", text: "12", correct: true },
          { letter: "E", text: "120", correct: false }
        ],
        hint: "$\\Delta h = 10,8 - 9 = 1,8\\text{ m}$. $v = \\sqrt{2g\\Delta h} = 6\\text{ m/s}$. $Q_m = \\rho \\cdot A \\cdot v$.",
        rationale: "Gabarito: <strong>D</strong>.<br>$v = \\sqrt{2 \\times 10 \\times 1,8} = 6\\text{ m/s}$.<br>$A = 20 \\times 10^{-4}\\text{ m}^2$.<br>$Q_m = 1.000 \\times 20 \\times 10^{-4} \\times 6 = 12\\text{ kg/s}$."
      },
      {
        id: 20,
        sourceNumber: 52,
        subject: "Dutos e Terminais",
        topic: "Termodinâmica / Ciclo de Carnot",
        statement: "Uma máquina térmica ideal retira $240\\text{ J}$ de calor da fonte quente a $627^{\\circ}\\text{C}$ e rejeita $80\\text{ J}$ para a fonte fria $T_F$. Qual é, em $^{\\circ}\\text{C}$, a temperatura da fonte fria?",
        options: [
          { letter: "A", text: "-273", correct: false },
          { letter: "B", text: "27", correct: true },
          { letter: "C", text: "327", correct: false },
          { letter: "D", text: "627", correct: false },
          { letter: "E", text: "900", correct: false }
        ],
        hint: "Converta $627^{\\circ}\\text{C}$ para Kelvin somando 273 ($900\\text{ K}$). $\\frac{Q_F}{Q_Q} = \\frac{T_F}{T_Q}$.",
        rationale: "Gabarito: <strong>B</strong>.<br>$T_Q = 627 + 273 = 900\\text{ K}$.<br>$\\frac{80}{240} = \\frac{1}{3} = \\frac{T_F}{900} \\implies T_F = 300\\text{ K} = 27^{\\circ}\\text{C}$."
      }
    ];

    const flashcardsData = [
      {
        title: "Comparação de Potências",
        category: "Matemática",
        formula: "$4^{37} = (2^2)^{37} = 2^{74} < 2^{75} = 8^{25} < 9^{25} = 3^{50}$",
        desc: "Iguale as bases ou encontre um expoente comum fatorando pelo MDC dos expoentes."
      },
      {
        title: "Vazão em Orifícios (Torricelli)",
        category: "Fluidos/Dutos",
        formula: "$v = \\sqrt{2g\\Delta h} \\quad \\text{e} \\quad Q_m = \\rho \\cdot A \\cdot v$",
        desc: "A velocidade na saída depende da coluna líquida líquida sobre o orifício."
      },
      {
        title: "Tubo de Venturi & Medição",
        category: "Fluidos/Dutos",
        formula: "$p_1 + \\frac{1}{2}\\rho v_1^2 = p_2 + \\frac{1}{2}\\rho v_2^2$",
        desc: "Ao reduzir a seção do duto, a velocidade aumenta e a pressão cai, medindo a vazão."
      },
      {
        title: "Aumentos Sucessivos",
        category: "Matemática",
        formula: "$V_{\\text{final}} = V_0 \\cdot (1 + i_1) \\cdot (1 + i_2) \\cdot (1 - d)$",
        desc: "Nunca some as porcentagens diretamente. Multiplique os fatores encadeados."
      },
      {
        title: "Ciclo de Carnot",
        category: "Fluidos/Dutos",
        formula: "$\\frac{Q_F}{Q_Q} = \\frac{T_F}{T_Q} \\quad (K = ^{\\circ}\\text{C} + 273)$",
        desc: "Lembre-se sempre de converter graus Celsius para Kelvin antes das divisões."
      },
      {
        title: "Desvio Padrão Nulo",
        category: "Matemática",
        formula: "$\\sigma = 0 \\iff x_1 = x_2 = \\dots = x_N$",
        desc: "Se todos os valores da amostra forem idênticos, a variabilidade é nula."
      }
    ];

    // ESTADO E PERSISTÊNCIA (LocalStorage)
    let activeFilter = 'TODAS';
    let currentQuestionsList = [...questionsDatabase];
    let currentIndexInFilter = 0;
    let userAnswers = JSON.parse(localStorage.getItem('transpetro_answers') || '{}');
    let showHint = false;
    let secondsElapsed = parseInt(localStorage.getItem('transpetro_time') || '0', 10);
    let timerInterval = null;
    let isTimerRunning = true;

    window.addEventListener('DOMContentLoaded', () => {
      startTimer();
      setSubjectFilter('TODAS');
      renderFlashcards();
      updateGlobalStats();
    });

    function startTimer() {
      if (timerInterval) clearInterval(timerInterval);
      timerInterval = setInterval(() => {
        if (isTimerRunning) {
          secondsElapsed++;
          localStorage.setItem('transpetro_time', secondsElapsed);
          const hrs = String(Math.floor(secondsElapsed / 3600)).padStart(2, '0');
          const mins = String(Math.floor((secondsElapsed % 3600) / 60)).padStart(2, '0');
          const secs = String(secondsElapsed % 60).padStart(2, '0');
          document.getElementById('timer-display').textContent = `${hrs}:${mins}:${secs}`;
        }
      }, 1000);
    }

    function toggleTimer() {
      isTimerRunning = !isTimerRunning;
      const btn = document.getElementById('timer-btn');
      btn.innerHTML = isTimerRunning ? '<i class="fa-solid fa-pause"></i>' : '<i class="fa-solid fa-play text-emerald-400"></i>';
    }

    function switchView(viewName) {
      document.getElementById('container-simulado').classList.add('hidden');
      document.getElementById('container-formulas').classList.add('hidden');
      document.getElementById('container-desempenho').classList.add('hidden');

      const tabs = ['simulado', 'formulas', 'desempenho'];
      tabs.forEach(t => {
        const el = document.getElementById(`view-tab-${t}`);
        el.className = "px-2.5 py-1 rounded-md text-[11px] sm:text-xs font-semibold text-slate-400 hover:text-white";
      });

      const activeBtn = document.getElementById(`view-tab-${viewName}`);
      activeBtn.className = "px-2.5 py-1 rounded-md text-[11px] sm:text-xs font-semibold bg-slate-800 text-emerald-400 border border-emerald-500/30";

      if (viewName === 'simulado') {
        document.getElementById('container-simulado').classList.remove('hidden');
      } else if (viewName === 'formulas') {
        document.getElementById('container-formulas').classList.remove('hidden');
        if (window.MathJax) MathJax.typesetPromise();
      } else if (viewName === 'desempenho') {
        document.getElementById('container-desempenho').classList.remove('hidden');
        updateGlobalStats();
      }
    }

    function toggleMobileNav() {
      const sidebar = document.getElementById('sidebar-nav');
      const isHidden = sidebar.classList.contains('hidden');
      sidebar.classList.toggle('hidden', !isHidden);
      document.getElementById('mobile-nav-toggle-text').textContent = isHidden ? "Fechar Grade" : "Ver Grade";
      if (isHidden) {
        sidebar.scrollIntoView({ behavior: 'smooth' });
      }
    }

    function setSubjectFilter(subject) {
      activeFilter = subject;

      const btns = {
        'TODAS': document.getElementById('btn-mat-todas'),
        'Português': document.getElementById('btn-mat-port'),
        'Matemática': document.getElementById('btn-mat-mat'),
        'Dutos e Terminais': document.getElementById('btn-mat-dutos')
      };

      for (let k in btns) {
        if (btns[k]) {
          btns[k].className = "subject-btn px-2.5 sm:px-3 py-1 rounded-lg text-[11px] sm:text-xs font-bold transition flex items-center gap-1.5 bg-slate-800 text-slate-300 border border-slate-700";
        }
      }

      if (subject === 'TODAS') {
        btns['TODAS'].className = "subject-btn px-2.5 sm:px-3 py-1 rounded-lg text-[11px] sm:text-xs font-bold transition flex items-center gap-1.5 bg-emerald-600 text-white shadow-sm ring-2 ring-emerald-400";
        currentQuestionsList = [...questionsDatabase];
        document.getElementById('badge-current-subject').innerHTML = `<i class="fa-solid fa-layer-group text-emerald-600"></i> Todas as Matérias`;
      } else if (subject === 'Português') {
        btns['Português'].className = "subject-btn px-2.5 sm:px-3 py-1 rounded-lg text-[11px] sm:text-xs font-bold transition flex items-center gap-1.5 bg-sky-600 text-white shadow-sm ring-2 ring-sky-400";
        currentQuestionsList = questionsDatabase.filter(q => q.subject === 'Português');
        document.getElementById('badge-current-subject').innerHTML = `<i class="fa-solid fa-book-open text-sky-600"></i> Português`;
      } else if (subject === 'Matemática') {
        btns['Matemática'].className = "subject-btn px-2.5 sm:px-3 py-1 rounded-lg text-[11px] sm:text-xs font-bold transition flex items-center gap-1.5 bg-amber-600 text-white shadow-sm ring-2 ring-amber-400";
        currentQuestionsList = questionsDatabase.filter(q => q.subject === 'Matemática');
        document.getElementById('badge-current-subject').innerHTML = `<i class="fa-solid fa-square-root-variable text-amber-600"></i> Matemática`;
      } else if (subject === 'Dutos e Terminais') {
        btns['Dutos e Terminais'].className = "subject-btn px-2.5 sm:px-3 py-1 rounded-lg text-[11px] sm:text-xs font-bold transition flex items-center gap-1.5 bg-purple-600 text-white shadow-sm ring-2 ring-purple-400";
        currentQuestionsList = questionsDatabase.filter(q => q.subject === 'Dutos e Terminais');
        document.getElementById('badge-current-subject').innerHTML = `<i class="fa-solid fa-gears text-purple-600"></i> Dutos & Terminais`;
      }

      currentIndexInFilter = 0;
      loadActiveQuestion();
      renderNavigationGrid();
    }

    function renderNavigationGrid() {
      const grid = document.getElementById('grid-buttons');
      grid.innerHTML = '';

      currentQuestionsList.forEach((q, idx) => {
        const btn = document.createElement('button');
        const answered = userAnswers[q.id];
        const isCurrent = idx === currentIndexInFilter;

        let style = "h-8 text-xs font-bold rounded-lg border transition-all flex items-center justify-center ";
        if (answered !== undefined) {
          const isCorrect = q.options.find(o => o.letter === answered)?.correct;
          style += isCorrect ? "bg-emerald-600 text-white border-emerald-700 shadow-sm" : "bg-rose-500 text-white border-rose-600 shadow-sm";
        } else {
          style += "bg-slate-100 text-slate-700 border-slate-200 active:bg-slate-200";
        }

        if (isCurrent) {
          style += " ring-2 ring-slate-900 ring-offset-1 font-extrabold scale-105 z-10";
        }

        btn.className = style;
        btn.textContent = q.sourceNumber;
        btn.onclick = () => {
          currentIndexInFilter = idx;
          loadActiveQuestion();
          if (window.innerWidth < 1024) {
            window.scrollTo({ top: 0, behavior: 'smooth' });
          }
        };
        grid.appendChild(btn);
      });

      document.getElementById('filtered-progress-tag').textContent = `${currentIndexInFilter + 1} / ${currentQuestionsList.length}`;
      document.getElementById('footer-index-display').textContent = currentIndexInFilter + 1;
      document.getElementById('footer-total-display').textContent = currentQuestionsList.length;
    }

    function loadActiveQuestion() {
      if (currentQuestionsList.length === 0) return;
      const q = currentQuestionsList[currentIndexInFilter];

      showHint = false;
      document.getElementById('box-hint').classList.add('hidden');
      document.getElementById('hint-label').textContent = "Dica";

      document.getElementById('card-q-number').textContent = `Questão ${q.sourceNumber}`;
      
      const subBadge = document.getElementById('card-q-subject');
      subBadge.textContent = q.subject;
      if (q.subject === 'Matemática') {
        subBadge.className = "text-xs font-bold px-2.5 py-1 rounded-lg bg-amber-100 text-amber-900 border border-amber-200";
      } else if (q.subject === 'Português') {
        subBadge.className = "text-xs font-bold px-2.5 py-1 rounded-lg bg-sky-100 text-sky-900 border border-sky-200";
      } else {
        subBadge.className = "text-xs font-bold px-2.5 py-1 rounded-lg bg-purple-100 text-purple-900 border border-purple-200";
      }

      document.getElementById('card-q-topic').textContent = q.topic;
      document.getElementById('content-statement').innerHTML = q.statement;
      document.getElementById('content-hint').innerHTML = q.hint;

      const boxContext = document.getElementById('box-context');
      if (q.context) {
        boxContext.classList.remove('hidden');
        document.getElementById('content-context').innerHTML = q.context.replace(/\n/g, '<br>');
      } else {
        boxContext.classList.add('hidden');
      }

      const container = document.getElementById('container-options');
      container.innerHTML = '';
      const answeredLetter = userAnswers[q.id];
      const hasAnswered = answeredLetter !== undefined;

      q.options.forEach(opt => {
        const btn = document.createElement('button');
        let style = "w-full text-left p-3.5 sm:p-4 rounded-xl border text-xs sm:text-sm font-medium transition-all flex items-start gap-3 touch-manipulation ";

        if (!hasAnswered) {
          style += "bg-white active:bg-slate-100 border-slate-200 text-slate-800 hover:border-slate-400";
        } else {
          if (opt.correct) {
            style += "bg-emerald-50 border-emerald-500 text-emerald-950 font-bold ring-1 ring-emerald-400";
          } else if (opt.letter === answeredLetter) {
            style += "bg-rose-50 border-rose-400 text-rose-950 ring-1 ring-rose-400";
          } else {
            style += "bg-white border-slate-200 text-slate-400 opacity-50";
          }
        }

        btn.className = style;
        btn.disabled = hasAnswered;
        btn.onclick = () => chooseAnswer(q.id, opt.letter);

        let badgeHtml = `<span class="w-7 h-7 shrink-0 rounded-full border border-slate-300 bg-slate-100 text-slate-700 flex items-center justify-center font-bold text-xs">${opt.letter}</span>`;
        if (hasAnswered) {
          if (opt.correct) {
            badgeHtml = `<span class="w-7 h-7 shrink-0 rounded-full bg-emerald-600 text-white flex items-center justify-center font-bold text-xs shadow-sm"><i class="fa-solid fa-check"></i></span>`;
          } else if (opt.letter === answeredLetter) {
            badgeHtml = `<span class="w-7 h-7 shrink-0 rounded-full bg-rose-500 text-white flex items-center justify-center font-bold text-xs shadow-sm"><i class="fa-solid fa-xmark"></i></span>`;
          }
        }

        btn.innerHTML = `
          ${badgeHtml}
          <div class="pt-0.5 leading-relaxed flex-1">${opt.text}</div>
        `;
        container.appendChild(btn);
      });

      const boxRationale = document.getElementById('box-rationale');
      if (hasAnswered) {
        const isCorrect = q.options.find(o => o.letter === answeredLetter)?.correct;
        boxRationale.className = `mt-5 p-4 sm:p-5 rounded-2xl border text-xs sm:text-sm leading-relaxed ${isCorrect ? 'bg-emerald-50/80 border-emerald-300 text-emerald-950' : 'bg-slate-50 border-slate-300 text-slate-800'}`;
        boxRationale.innerHTML = `
          <div class="flex items-center gap-2 font-bold mb-2 uppercase tracking-wider text-xs ${isCorrect ? 'text-emerald-700' : 'text-slate-700'}">
            <i class="${isCorrect ? 'fa-solid fa-circle-check text-emerald-600 text-base' : 'fa-solid fa-circle-xmark text-rose-500 text-base'}"></i>
            ${isCorrect ? 'Você acertou!' : 'Resposta Incorreta. Veja a resolução:'}
          </div>
          <div>${q.rationale}</div>
        `;
        boxRationale.classList.remove('hidden');
      } else {
        boxRationale.classList.add('hidden');
      }

      document.getElementById('btn-prev-question').disabled = currentIndexInFilter === 0;
      document.getElementById('btn-prev-question').classList.toggle('opacity-30', currentIndexInFilter === 0);

      renderNavigationGrid();
      if (window.MathJax) MathJax.typesetPromise();
    }

    function chooseAnswer(questionId, letter) {
      userAnswers[questionId] = letter;
      localStorage.setItem('transpetro_answers', JSON.stringify(userAnswers));
      loadActiveQuestion();
      updateGlobalStats();
    }

    function navigateQuestion(step) {
      const nextIdx = currentIndexInFilter + step;
      if (nextIdx >= 0 && nextIdx < currentQuestionsList.length) {
        currentIndexInFilter = nextIdx;
        loadActiveQuestion();
        if (window.innerWidth < 1024) {
          window.scrollTo({ top: 0, behavior: 'smooth' });
        }
      }
    }

    function toggleHint() {
      showHint = !showHint;
      document.getElementById('box-hint').classList.toggle('hidden', !showHint);
      document.getElementById('hint-label').textContent = showHint ? "Fechar" : "Dica";
    }

    function resetAnswers() {
      if (confirm("Deseja apagar todas as respostas e zerar seu placar do simulado?")) {
        userAnswers = {};
        localStorage.removeItem('transpetro_answers');
        loadActiveQuestion();
        updateGlobalStats();
      }
    }

    function updateGlobalStats() {
      const totalQuestions = questionsDatabase.length;
      let totalAnswered = 0;
      let totalCorrect = 0;

      const subStats = {
        'Português': { total: 0, answered: 0, correct: 0 },
        'Matemática': { total: 0, answered: 0, correct: 0 },
        'Dutos e Terminais': { total: 0, answered: 0, correct: 0 }
      };

      questionsDatabase.forEach(q => {
        if (subStats[q.subject]) subStats[q.subject].total++;
        if (userAnswers[q.id] !== undefined) {
          totalAnswered++;
          if (subStats[q.subject]) subStats[q.subject].answered++;
          const correctOpt = q.options.find(o => o.correct);
          if (correctOpt && correctOpt.letter === userAnswers[q.id]) {
            totalCorrect++;
            if (subStats[q.subject]) subStats[q.subject].correct++;
          }
        }
      });

      const overallAccuracy = totalAnswered > 0 ? Math.round((totalCorrect / totalAnswered) * 100) : 0;

      document.getElementById('top-accuracy-badge').textContent = `${overallAccuracy}%`;
      document.getElementById('count-todas').textContent = totalQuestions;
      document.getElementById('count-port').textContent = subStats['Português'].total;
      document.getElementById('count-mat').textContent = subStats['Matemática'].total;
      document.getElementById('count-dutos').textContent = subStats['Dutos e Terminais'].total;

      const pAcc = subStats['Português'].total > 0 ? Math.round((subStats['Português'].correct / subStats['Português'].total) * 100) : 0;
      document.getElementById('score-port').textContent = `${subStats['Português'].correct}/${subStats['Português'].total} (${pAcc}%)`;
      document.getElementById('bar-port').style.width = `${pAcc}%`;

      const mAcc = subStats['Matemática'].total > 0 ? Math.round((subStats['Matemática'].correct / subStats['Matemática'].total) * 100) : 0;
      document.getElementById('score-mat').textContent = `${subStats['Matemática'].correct}/${subStats['Matemática'].total} (${mAcc}%)`;
      document.getElementById('bar-mat').style.width = `${mAcc}%`;

      const dAcc = subStats['Dutos e Terminais'].total > 0 ? Math.round((subStats['Dutos e Terminais'].correct / subStats['Dutos e Terminais'].total) * 100) : 0;
      document.getElementById('score-dutos').textContent = `${subStats['Dutos e Terminais'].correct}/${subStats['Dutos e Terminais'].total} (${dAcc}%)`;
      document.getElementById('bar-dutos').style.width = `${dAcc}%`;

      document.getElementById('stat-total-percent').textContent = `${overallAccuracy}%`;
      document.getElementById('stat-total-detail').textContent = `${totalCorrect} acertos de ${totalAnswered} resolvidas`;
      document.getElementById('stat-answered-count').textContent = `${totalAnswered} / ${totalQuestions}`;
      document.getElementById('stat-remaining-count').textContent = totalQuestions - totalAnswered;
      document.getElementById('stat-points').textContent = `${(totalCorrect * 1.0).toFixed(1)} pts`;

      const statsBars = document.getElementById('stats-subject-bars');
      statsBars.innerHTML = '';
      for (const [subj, data] of Object.entries(subStats)) {
        const pct = data.answered > 0 ? Math.round((data.correct / data.answered) * 100) : 0;
        const barDiv = document.createElement('div');
        barDiv.className = "bg-slate-50 p-3 sm:p-4 rounded-xl border border-slate-200";
        barDiv.innerHTML = `
          <div class="flex justify-between text-xs font-bold mb-1.5">
            <span class="text-slate-800">${subj}</span>
            <span class="text-emerald-700">${data.correct} acertos (${pct}%)</span>
          </div>
          <div class="w-full bg-slate-200 rounded-full h-2.5 overflow-hidden">
            <div class="bg-emerald-600 h-2.5 rounded-full transition-all duration-300" style="width: ${pct}%"></div>
          </div>
        `;
        statsBars.appendChild(barDiv);
      }
    }

    function renderFlashcards(filter = 'TODOS') {
      const container = document.getElementById('flashcards-grid');
      container.innerHTML = '';
      const list = filter === 'TODOS' ? flashcardsData : flashcardsData.filter(f => f.category === filter);

      list.forEach(card => {
        const el = document.createElement('div');
        el.className = "bg-white p-4 sm:p-5 rounded-2xl border border-slate-200 shadow-sm flex flex-col justify-between";
        el.innerHTML = `
          <div>
            <span class="text-[9px] font-bold uppercase tracking-wider px-2 py-0.5 rounded bg-slate-100 text-slate-700 border border-slate-200">
              ${card.category}
            </span>
            <h4 class="font-bold text-slate-900 text-xs sm:text-sm mt-2 mb-1.5">${card.title}</h4>
            <div class="bg-slate-50 p-2.5 rounded-xl text-xs font-mono text-slate-900 border border-slate-100 mb-2 text-center overflow-x-auto">
              ${card.formula}
            </div>
            <p class="text-xs text-slate-600 leading-relaxed">${card.desc}</p>
          </div>
        `;
        container.appendChild(el);
      });
      if (window.MathJax) MathJax.typesetPromise();
    }

    function filterFlashcards(cat) {
      renderFlashcards(cat);
    }
  </script>
</body>
</html>
