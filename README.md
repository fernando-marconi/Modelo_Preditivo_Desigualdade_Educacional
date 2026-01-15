# Modelagem Preditiva da Desigualdade Educacional: Identificando Fatores de Elite no ENEM BH

Este repositório apresenta o desenvolvimento de um modelo de Inteligência Artificial voltado à predição de alta performance acadêmica no município de Belo Horizonte, utilizando os microdados do ENEM 2024. O projeto foca na transição da análise descritiva para a ciência de dados preditiva, buscando identificar os fatores estruturais que determinam a entrada de um estudante no Decil 10 (as 10% maiores notas).

---

## Metodologia e Processamento de Dados

O modelo utiliza como base os dados consolidados na **Camada Ouro** da arquitetura de medalhões, garantindo que as informações de entrada tenham passado por etapas prévias de limpeza, padronização e filtragem geográfica.

### Engenharia de Atributos (Feature Engineering)
Para viabilizar o treinamento do algoritmo e garantir a qualidade das predições, foram aplicadas as seguintes transformações:
* **Target Binário:** A variável alvo foi convertida em uma classificação binária, onde o valor 1 representa alunos pertencentes ao Decil 10 em Ciências Humanas e o valor 0 representa os demais decis.
* **Codificação Categórica (One-Hot Encoding):** Atributos como rede administrativa (`tp_adm_escola`), tipo de escola (`tipo_escola_agrupada`) e idioma estrangeiro foram transformados em vetores binários através da função `pd.get_dummies()`.
* **Tratamento de Dados Ausentes:** Implementação de preenchimento de valores nulos com a categoria "NAO_INFORMADO", assegurando a integridade do processamento matemático pelo estimador.

---

## Implementação do Modelo de Aprendizado de Máquina

O algoritmo selecionado para este estudo foi o **Random Forest Classifier** (Floresta Aleatória). Esta escolha fundamenta-se na capacidade do modelo de lidar com variáveis categóricas complexas e identificar relações não-lineares sem a necessidade de normalização rigorosa dos dados.



### Configuração e Parâmetros de Treinamento
* **Estimadores:** Configuração de 100 árvores de decisão independentes (`n_estimators=100`) para promover a estabilidade da predição e reduzir o risco de sobreajuste (*overfitting*).
* **Estratificação:** Divisão dos dados em 80% para treinamento e 20% para teste, utilizando o parâmetro `stratify=y` para preservar a proporção da classe de elite (minoritária) em ambos os conjuntos.
* **Balanceamento de Classes:** Aplicação do parâmetro `class_weight='balanced'`, técnica essencial para datasets desbalanceados que força o algoritmo a atribuir importância equivalente às classes elite e não-elite durante o ajuste dos pesos.

---

## Avaliação de Performance e Interpretabilidade

### Validação por Matriz de Confusão
A eficácia do modelo foi validada através da análise de erros e acertos no conjunto de teste:
* **Verdadeiros Positivos:** O modelo identificou corretamente 247 estudantes de elite.
* **Falsos Negativos:** Houve apenas 22 casos onde o modelo falhou em identificar um aluno de elite, indicando uma alta sensibilidade (*recall*) para o fenômeno estudado.
![Matriz de Confusão](graficos/matriz_confusao.png)


### Importância das Variáveis (Feature Importance)
A análise de pesos revela a hierarquia dos fatores preditivos no desempenho escolar em Belo Horizonte:
* **Rede Estadual:** Identificada como o principal preditor, detendo um peso de aproximadamente 50% na decisão do modelo.
* **Rede Privada:** Consolida-se como o segundo fator de maior influência, reafirmando que a dependência administrativa é o filtro estrutural mais rígido no acesso ao topo da pirâmide de notas.
* **Fatores Secundários:** A escolha do idioma estrangeiro e a localização da escola apresentam pesos significativamente menores, indicando que, no contexto de BH, a rede de ensino prevalece sobre a localização geográfica.
![Importância das Variáveis](graficos/importância_variaveis.png)

---

## Conclusões Técnicas

Os resultados demonstram que o desempenho de elite no ENEM em Belo Horizonte é altamente previsível através de variáveis estruturais e administrativas. O modelo de Machine Learning obteve sucesso em "aprender" os padrões de desigualdade, servindo como ferramenta diagnóstica para identificar onde os gargalos de conversão de talentos são mais acentuados. Do ponto de vista de portfólio, este projeto comprova proficiência em Engenharia de Atributos, Treinamento de Modelos Robustos e Interpretabilidade de IA Aplicada.
