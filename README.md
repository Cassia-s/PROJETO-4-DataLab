# Projeto de Análise de Dados

## Título do Projeto: “DataLab”

<details>
  <summary><strong>Visão Geral do Projeto</strong></summary>
  <p>Este projeto, denominado "DataLab", teve como objetivo principal analisar dados financeiros históricos de ações de grandes empresas de tecnologia. A análise visou identificar padrões de volatilidade, volume de negociação e consistência nos preços, gerando segmentações por perfil de risco para auxiliar investidores de diversos perfis (conservador, moderado, agressivo) em suas decisões de investimento.</p>
</details>

<details>
  <summary><strong>Ferramentas e Tecnologias</strong></summary>
  <ul>
    <li>Ambiente de Desenvolvimento: Google Colab</li>
    <li>Linguagem de Programação: Python</li>
    <li>Visualização e Dashboards: Looker Studio</li>
    <li>Validação de Códigos: Chat GPT e Gemini</li>
  </ul>
</details>

<details>
  <summary><strong>Equipe</strong></summary>
  <ul>
    <li>Cassia Silva</li>
    <li>Vanessa Santana</li>
  </ul>
</details>

<details>
  <summary><strong>Processamento da Base de Dados</strong></summary>
  <p>O projeto utilizou dois arquivos de dados principais:</p>
  <ul>
    <li><code>big_tech_companies.csv</code>: Contém os símbolos das ações e nomes das empresas.</li>
    <li><code>big_tech_stock_prices.xlsx</code>: Histórico diário de preços (open, high, low, close, adj_close) e volume de negociação.</li>
  </ul>
  <p>Ambos foram carregados no ambiente do Google Colab (Projeto_4.ipynb).</p>

  <h4>Etapas de Tratamento de Dados:</h4>
  <ul>
    <li><strong>Verificação Inicial:</strong> Importação bem-sucedida, verificação e conversão dos tipos de dados, com datas convertidas para o formato datetime e validadas.</li>
    <li><strong>Limpeza de Dados:</strong> Uma linha com valores nulos foi identificada e removida. Adicionalmente, uma linha duplicada foi removida, resultando em uma base de dados final limpa e consistente. Não foram encontrados valores fora do escopo (como preço ou volume ≤ 0) nem categorias inválidas na coluna <code>stock_symbol</code>. As datas analisadas abrangeram o intervalo de 2010-01-04 a 2023-01-24.</li>
    <li><strong>Padronização:</strong> A coluna <code>stock_symbol</code> foi padronizada para letras maiúsculas, e a distribuição de registros por empresa foi verificada, confirmando a representação das 14 empresas.</li>
    <li><strong>Análise de Outliers:</strong> A detecção de outliers foi realizada utilizando o método do Intervalo Interquartil (IQR). Outliers foram identificados nas variáveis `open` (2.553 registros), `high` (2.594 registros), `low` (2.514 registros), `close` (2.555 registros), `adj_close` (3.333 registros) e `volume` (3.462 registros). Optou-se por manter esses outliers, pois eles representam eventos históricos legítimos do mercado, como ganhos extraordinários da Netflix ou o lançamento do iPad pela Apple, que são informações relevantes para a análise.</li>
  </ul>

  <h4>Variáveis Criadas:</h4>
  <p>Para aprimorar a análise, foram criadas diversas variáveis derivadas a partir dos dados originais:</p>
  <ul>
    <li><code>variação_diaria</code></li>
    <li><code>pct_var</code> (variação percentual)</li>
    <li><code>subiu</code> (indicador booleano para dias de alta)</li>
    <li><code>subiu_5pct</code> (indicador para dias com alta de 5% ou mais)</li>
    <li>Médias móveis (de 5 e 20 dias)</li>
    <li>Desvio padrão de 5 dias</li>
    <li><code>amplitude_diaria</code></li>
    <li><code>volatilidade relativa</code></li>
    <li><code>gap_abertura</code></li>
    <li><code>perfil_risco</code> (categorizado como Conservador, Moderado, Agressivo)</li>
  </ul>
</details>

<details>
  <summary><strong>Análise Exploratória de Dados (EDA)</strong></summary>
  <p>A etapa de EDA focou na compreensão da distribuição, padrões e tendências dos preços das ações, além da criação de novas variáveis para aprofundar a análise.</p>
  <ul>
    <li><strong>Distribuição de Preços:</strong> A análise por meio de boxplots revelou alta volatilidade nas ações de empresas como TSLA, META e NFLX. Em contraste, IBM, INTC e ORCL demonstraram maior estabilidade nos preços.</li>
    <li><strong>Volume de Negociação:</strong> AAPL, AMZN e GOOGL apresentaram os maiores volumes médios de negociação. Foi observado que um alto volume não se correlaciona diretamente com a volatilidade dos preços.</li>
    <li><strong>Medidas de Tendência Central:</strong> Foram comparadas a média e a mediana. Em ações mais voláteis, a mediana se mostrou mais representativa do que a média.</li>
    <li><strong>Dispersão:</strong> Métricas como desvio padrão, variância e Intervalo Interquartil (IQR) foram calculadas para todas as variáveis. Empresas com um desvio padrão elevado exibiram maior risco.</li>
    <li><strong>Correlação:</strong> Uma forte correlação foi identificada entre as variáveis `open`, `close`, `high` e `low`, indicando consistência nos dados de preço. No entanto, o volume apresentou baixa correlação com os preços, sugerindo um comportamento mais independente.</li>
    <li><strong>Risco Relativo:</strong> O conceito de risco relativo foi empregado para comparar dias com alta igual ou superior a 5%.</li>
  </ul>
</details>

<details>
  <summary><strong>Segmentação por Perfil de Investidor</strong></summary>
  <p>A segmentação das empresas por perfil de investidor foi realizada com base em critérios como Amplitude de Preço, Desvio Padrão e Volume Médio, resultando nas seguintes classificações:</p>
  <table>
    <thead>
      <tr>
        <th>Perfil</th>
        <th>Empresas Identificadas</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Conservador</td>
        <td>IBM, ORCL, INTC</td>
      </tr>
      <tr>
        <td>Moderado</td>
        <td>AAPL, MSFT, GOOGL, ADBE</td>
      </tr>
      <tr>
        <td>Agressivo</td>
        <td>TSLA, META, NFLX, NVDA, CRM</td>
      </tr>
    </tbody>
  </table>
</details>

<details>
  <summary><strong>Validação de Hipótese</strong></summary>
  <p>Foi realizada a validação da hipótese: "Ações com maior volume médio de negociação são mais voláteis (maior desvio padrão de preço)".</p>

  <h4>Método:</h4>
  <p>As empresas foram divididas em dois grupos: alto volume versus baixo volume, com a mediana do volume de negociação servindo como critério de separação. O desvio padrão dos preços de fechamento (`close`) entre esses dois grupos foi então comparado usando um teste t para amostras independentes.</p>

  <h4>Resultados:</h4>
  <table>
    <thead>
      <tr>
        <th>Métrica</th>
        <th>Valor</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Estatística t</td>
        <td>-0.7895</td>
      </tr>
      <tr>
        <td>Valor-p</td>
        <td>0.4527</td>
      </tr>
      <tr>
        <td>Média do desvio padrão (alto volume)</td>
        <td>57.63</td>
      </tr>
      <tr>
        <td>Média do desvio padrão (baixo volume)</td>
        <td>80.55</td>
      </tr>
    </tbody>
  </table>

  <h4>Conclusão da Hipótese:</h4>
  <p>Dado que o valor-p (0.4527) é maior que 0.05, não há diferença estatística significativa entre as médias dos desvios padrão dos grupos. Portanto, a hipótese de que empresas com maior volume de negociação são mais voláteis não foi sustentada pelos dados. Isso reforça a ideia de que um alto volume de negociação não implica necessariamente um maior risco de volatilidade de preços. Em termos mais simples: "Ter um maior número de negociações não significa que o preço de uma ação mudará mais. Algumas empresas com menos movimento de negociação ainda podem ser mais instáveis em seus preços."</p>
</details>

<details>
  <summary><strong>Modelagem Preditiva</strong></summary>

  <h4>Regressão Linear (5.1) – MARCO 2:</h4>
  <p><strong>Objetivo:</strong> Modelar a relação entre o volume de negociação (`volume`) e o preço de fechamento (`close`) para determinar se existe uma dependência linear que permita prever o preço.</p>

  <p><strong>Resultados do Modelo:</strong></p>
  <table>
    <thead>
      <tr>
        <th>Métrica</th>
        <th>Valor</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Coeficiente (volume)</td>
        <td>-0.000000</td>
      </tr>
      <tr>
        <td>Intercepto</td>
        <td>102.24</td>
      </tr>
      <tr>
        <td>R² (Coeficiente de Determinação)</td>
        <td>0.0505</td>
      </tr>
      <tr>
        <td>Erro Padrão (RMSE)</td>
        <td>98.99</td>
      </tr>
    </tbody>
  </table>

  <p><strong>Interpretação:</strong> O coeficiente do volume muito próximo de zero indica que o volume de negociação tem pouquíssima ou nenhuma influência direta sobre o preço de fechamento. O valor de $R^2$ de $0.0505$ é extremamente baixo, sugerindo que o modelo explica apenas cerca de 5% da variância no preço de fechamento, o que é um indicador de baixa capacidade preditiva.</p>
  <p><strong>Conclusão:</strong> A relação linear entre volume e preço de fechamento é muito fraca. O volume não se mostra um bom preditor do preço das ações para o período analisado utilizando este modelo de regressão linear.</p>

  <h4>Regressão Logística (5.2) – MARCO 2:</h4>
  <p><strong>Objetivo:</strong> Prever a probabilidade de uma ação fechar em alta (`close > open`), utilizando o volume negociado como variável preditora.</p>

  <p><strong>Matriz de Confusão e Classificação:</strong></p>
  <table>
    <thead>
      <tr>
        <th>Métrica</th>
        <th>Classe "Não Subiu" (0)</th>
        <th>Classe "Subiu" (1)</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Precision</td>
        <td>0.51</td>
        <td>0.52</td>
      </tr>
      <tr>
        <td>Recall</td>
        <td>0.71</td>
        <td>0.31</td>
      </tr>
      <tr>
        <td>F1-score</td>
        <td>0.59</td>
        <td>0.39</td>
      </tr>
    </tbody>
  </table>

  <p>Após aplicar técnicas de balanceamento de classes e criar novas variáveis derivadas, o modelo de regressão logística apresentou melhora significativa de desempenho:</p>
  <ul>
    <li>O modelo passou a identificar corretamente parte dos dias em que a ação sobe, o que não ocorria na versão anterior (F1-score = 0).</li>
    <li>Apesar de ainda apresentar dificuldades com a classe positiva, os resultados indicam uma evolução considerável.</li>
    <li>Recall (classe “subiu”) = 0.31 → o modelo acerta 31% dos dias com alta real.</li>
    <li>F1-score (classe “subiu”) = 0.39 → há poder preditivo legítimo, mesmo que ainda inicial.</li>
  </ul>
  <p><strong>Conclusão:</strong> Com o balanceamento adequado das classes e uma engenharia de atributos mais rica, a regressão logística evoluiu de um modelo ineficaz para uma versão básica, porém funcional. Essa melhoria comprova que a qualidade das variáveis e o equilíbrio das classes são fatores cruciais na construção de modelos preditivos eficazes.</p>
</details>

<details>
  <summary><strong>Conclusões Gerais</strong></summary>
  <ul>
    <li>A análise estatística e visual realizada permitiu a clara identificação de perfis de risco entre as empresas estudadas.</li>
    <li>A segmentação das empresas por perfil de risco oferece um suporte valioso na recomendação de ações, equilibrando segurança e potencial de retorno.</li>
    <li>A aplicação de testes estatísticos, como o teste t, conferiu maior rigor e confiabilidade às conclusões obtidas.</li>
    <li>A regressão linear demonstrou que o volume de negociação possui uma baixa relação com o preço das ações, indicando que não é um preditor relevante por si só.</li>
    <li>A regressão logística revelou que o volume não é suficiente, por si só, para prever com alta precisão se uma ação subirá em um determinado dia.</li>
    <li>Foi concluído que o volume e a volatilidade das ações são variáveis independentes no contexto da análise realizada.</li>
    <li>Modelos preditivos simples que utilizam apenas o volume como variável explicativa são pouco eficazes. Sugere-se que outras variáveis, como fundamentos da empresa e eventos externos do mercado, são mais relevantes para a previsão do comportamento dos preços das ações.</li>
</details>

<details>
  <summary><strong>Links</strong></summary>
  <ul>
    <li><a href="https://lookerstudio.google.com/reporting/184f019b-ae3f-4cc3-bbd8-35313b405b99">Apresentação Looker Studio</a></li>
    <li><a href="https://www.loom.com/share/46db364c831e4ea7aa492cf1b3926727">Apresentação de vídeo (Loom)</a></li>
  </ul>
</details>

