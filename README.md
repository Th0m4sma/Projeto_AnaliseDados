# RELATÓRIO FINAL (ANÁLISE DE DADOS)

Diante das dificuldades observadas no desempenho dos alunos em provas, foi disponibilizada uma base de dados contendo informações sobre estudantes, suas performances e hábitos relacionados ao período que antecede o exame final. 
Essa base foi obtida no site Kaggle [(Student Performance Factors Dataset)](https://www.kaggle.com/datasets/fatihyavuzz/studentperformancefactors), 
uma plataforma que não só fornece bases de dados, mas também disponibiliza ferramentas para aprimorar habilidades e aplicar conhecimentos aprendidos. Nos propomos a analisar a base de dados, preparando o ambiente e importando as bibliotecas necessárias para o processo:
- `pip install pandas`
- `pip install numpy`
- `pip install matplotlib`
- `pip install ydata-profiling`
- `pip install scikit-learn`

Em seguida importamos nossa base de dados utilizando a biblioteca `pandas` e geramos uma pequena visualização:

| Hours_Studied | Attendance | Parental_Involvement | Access_to_Resources | Extracurricular_Activities | Sleep_Hours | Previous_Scores | Motivation_Level | Internet_Access | Tutoring_Sessions | Family_Income | Teacher_Quality | School_Type | Peer_Influence | Physical_Activity | Learning_Disabilities | Parental_Education_Level | Distance_from_Home | Gender | Exam_Score |
|---------------|------------|----------------------|---------------------|----------------------------|-------------|------------------|------------------|-----------------|-------------------|---------------|-----------------|-------------|----------------|-------------------|------------------------|-------------------------|--------------------|--------|------------|
| 23            | 84         | Low                  | High                | No                         | 7           | 73               | Low              | Yes             | 0                 | Low           | Medium          | Public     | Positive      | 3                 | No                     | High School             | Near               | Male   | 67         |
| 19            | 64         | Low                  | Medium              | No                         | 8           | 59               | Low              | Yes             | 2                 | Medium        | Medium          | Public     | Negative      | 4                 | No                     | College                | Moderate           | Female | 61         |
| 24            | 98         | Medium               | Medium              | Yes                        | 7           | 91               | Medium            | Yes             | 2                 | Medium        | Medium          | Public     | Neutral       | 4                 | No                     | Postgraduate           | Near               | Male   | 74         |
| 29            | 89         | Low                  | Medium              | Yes                        | 8           | 98               | Medium            | Yes             | 1                 | Medium        | Medium          | Public     | Negative      | 4                 | No                     | High School            | Moderate           | Male   | 71         |
| 19            | 92         | Medium               | Medium              | Yes                        | 6           | 65               | Medium            | Yes             | 3                 | Medium        | High            | Public     | Neutral       | 4                 | No                     | College                | Near               | Female | 70         |
>A base de dados apresenta 20 colunas, das quais 7 possuem valores numéricos, enquanto as demais contêm dados textuais ou categóricos. 

Cada coluna representa um aspecto relevante para análise, conforme descrito a seguir:
- "Hours Studied" – Número de horas que o aluno estudou
- "Attendance" - Taxa de frequência ou porcentagem de aulas frequentadas pelo aluno
- "Parental_Involvement" - Nível de envolvimento dos pais na vida acadêmica do aluno
- "Access_to_Resources" - Disponibilidade de recursos educacionais para o aluno
- "Extracurricular_Activities" - Participação em atividades extracurriculares
- "Sleep_Hours" - Número médio de horas que o aluno dorme por noite
- "Previous_Scores" - Notas ou desempenhos acadêmicos anteriores do aluno
- "Motivation_Level" - Nível de motivação do aluno em relação aos objetivos acadêmicos
- "Internet_Access" - Indica se o aluno tem acesso à internet (Yes/No)
- "Tutoring_Sessions" – Número de sessões de tutoria ou mentoria frequentadas pelo aluno
- "Family_Income" - Nível de renda da família do aluno
- "Teacher_Quality" - Qualidade percebida dos professores (por exemplo, avaliada por experiência ou feedback)
- "School_Type" - Tipo de escola que o aluno frequenta (por exemplo, pública, privada)
- "Peer_Influence" - Nível de influência dos colegas no desempenho acadêmico do aluno
- "Physical_Activity" - Quantidade de atividade física realizada pelo aluno
- "Learning_Disabilities" - Indica se o aluno tem alguma deficiência de aprendizado (Sim/Não)
- "Parental_Education_Level" - Nível de escolaridade dos pais do aluno
- "Distance_from_Home" - Distância entre a casa do aluno e a escola
- "Gender" - Gênero do aluno
- "Exam_Score" - Nota do aluno em um exame recente



## PREPARANDO DADOS
Ao analisar mais profundamente nossa base de dados, identificamos a presença de valores vazios em algumas linhas. 
Para lidar com isso, optamos por eliminar todas as linhas que apresentassem algum campo vazio. Essa operação foi realizada utilizando o seguinte comando da biblioteca 
Pandas no Python: `dataset.dropna(inplace=True)`. Após executar este comando, houve uma redução no número de linhas na base de dados. Inicialmente, o dataset possuía 6607 linhas, mas, após a remoção, passaram a restar 6378 linhas, 
garantindo que não houvesse mais campos vazios. Além disso, realizamos uma alteração nos nomes das colunas da tabela, com o objetivo de tornar os dados mais intuitivos e facilitar futuras análises. 
Além disso, realizamos uma alteração nos nomes das colunas da tabela, com o objetivo de tornar os dados mais intuitivos e facilitar futuras análises. As novas colunas ficaram assim: 
- "Hours Studied" – "Horas_Estudo"
- "Attendance" – "Presenca"
- "Parental_Involvement" – "Envolvimento_Pais"
- "Access_to_Resources" – "Acesso_Recursos"
- "Extracurricular_Activities" – "Atividade_Extracurricular"
- "Sleep_Hours" – "Horas_Sono"
- "Previous_Scores" – "Pontuacao_Anterior"
- "Motivation_Level" – "Nivel_Motivacao"
- "Internet_Access" – "Acesso_Internet"
- "Tutoring_Sessions" – "Tutoria"
- "Family_Income" – "Renda_Familiar"
- "Teacher_Quality" – "Qualidade_Ensino"
- "School_Type" – "Tipo_Escola"
- "Peer_Influence" – "Influencia_Colegas"
- "Physical_Activity" – "Atividade_Fisica"
- "Learning_Disabilities" – "Deficiencia_Aprendizagem"
- "Parental_Education_Level" – "Educacao_Pais"
- "Distance_from_Home" – "Distancia_EscolaCasa"
- "Gender" – "Genero"
- "Exam_Score" – "Pontuacao_Final"

Após realizar essas modificações, utilizamos uma ferramenta para gerar um relatório dos dados com o objetivo de obter insights iniciais e ideias para análises futuras.
Para isso, utilizamos a biblioteca `y-data_profiling`, que oferece a função `ProfileReport`. Essa função gera um documento em formato HTML contendo resumos das variáveis e insights interessantes sobre o conjunto de dados.

A partir da leitura do nosso relatório, gerado acima, conseguimos observar alguns insights relevantes a serem realizados, como:

- Comparar o desempenhos dos participantes de diferentes gêneros no exame.
- Análisar a influência das horas de sono no desemepenho dos participantes.
- Análisar a influência das horas de estudo no desemepenho dos participantes.
- Entender e comparar o desempenho dos participantes de tipos de ensinos diferentes.
- Verificar se realmente a presença nas aulas influência no desempenho do aluno.
- Análisar o desempenho de participantes com niveis de motivação diferente.
Por fim, seria interessante o desenvolvimento de uma análise sobre os 150 maiores pontuadores no exame final, a fim de verificar que fatores/habitos são comuns entre eles.
