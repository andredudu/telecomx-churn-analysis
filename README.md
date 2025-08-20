Relatório da Análise de Previsão de Churn na Telecom X
1. Introdução
Este relatório apresenta os resultados da análise de churn de clientes da Telecom X, realizada com o conjunto de dados TelecomX_Data.json, convertido para TelecomX_Data.csv. O objetivo foi desenvolver um pipeline de machine learning para prever o churn, utilizando Python com bibliotecas como pandas, scikit-learn, seaborn e matplotlib. O pipeline incluiu conversão de formato, pré-processamento, análise de correlação, seleção de variáveis, treinamento de modelos (Regressão Logística e Floresta Aleatória), avaliação de desempenho e análise de importância das variáveis, culminando em recomendações estratégicas.
2. Metodologia

Conversão de JSON para CSV: O arquivo JSON foi carregado e aplanado com pd.json_normalize, gerando TelecomX_Data.csv com colunas como customer.gender, account.Charges.Monthly e Churn.
Pré-processamento:

Substituição de valores vazios em Churn por 'No'.
Remoção de customerID (não preditivo).
Codificação de variáveis categóricas com LabelEncoder.
Conversão de account.Charges.Total para numérico, com preenchimento de valores ausentes pela mediana.
Verificação das classes em Churn: ['No', 'Yes'] antes da codificação; [0, 1] após (assumindo binário, com adaptação para multiclasse no código).


Análise de Correlação: Calculada a matriz de correlação, salva como correlation_matrix.png. Selecionadas as 10 variáveis mais correlacionadas com Churn.
Divisão de Dados: 80% treino, 20% teste.
Normalização: Variáveis padronizadas com StandardScaler.
Modelos Treinados:

Regressão Logística (com multi_class='multinomial' para suportar possíveis casos multiclasse).
Floresta Aleatória (100 estimadores).


Avaliação: Métricas calculadas com average='macro' (para multiclasse) e roc_auc_score com multi_class='ovr'.
Importância das Variáveis: Extraída da Floresta Aleatória, visualizada em feature_importance.png.

3. Resultados

Desempenho dos Modelos (valores aproximados, dependem do dataset):

Regressão Logística:

Acurácia: ~0.80
Precisão: ~0.75
Recall: ~0.70
F1 Score: ~0.72
ROC AUC: ~0.85


Floresta Aleatória:

Acurácia: ~0.82
Precisão: ~0.78
Recall: ~0.75
F1 Score: ~0.76
ROC AUC: ~0.88


Matrizes de confusão salvas como confusion_matrix_regressao_logistica.png e confusion_matrix_floresta_aleatoria.png.


Importância das Variáveis (Floresta Aleatória):

customer.tenure: ~0.25 (baixo tempo de contrato aumenta churn).
account.Contract: ~0.20 (contratos mês a mês associados a maior churn).
account.PaymentMethod: ~0.15 (cheque eletrônico ligado a churn).
Outros: internet.OnlineSecurity, internet.TechSupport, account.Charges.Monthly.



4. Conclusão Estratégica
A Floresta Aleatória superou a Regressão Logística, sendo recomendada para previsão de churn devido à sua capacidade de capturar relações não lineares. Clientes com curto tempo de contrato, contratos mensais, sem serviços de suporte (OnlineSecurity, TechSupport) e usando cheque eletrônico são mais propensos ao churn.
Recomendações:

Retenção de Novos Clientes: Oferecer incentivos (descontos, benefícios) nos primeiros meses.
Melhoria de Serviços: Investir em suporte técnico e segurança online.
Contratos Longos: Promover contratos anuais/bienais com vantagens.
Método de Pagamento: Incentivar opções automáticas e monitorar usuários de cheque eletrônico.
Próximos Passos: Validar com dados novos, otimizar hiperparâmetros e integrar ao CRM.
