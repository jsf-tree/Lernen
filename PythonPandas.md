>>>> Substituir valores -> utilizar loc ou iloc
df.iloc[0, 3] = 'asd' <- substitui 1a linha da 4a coluna por 'asd'
df.iloc[:, 3] = 'asd' <- substitui todos os valores da 4a coluna por 'asd'
iloc -> valores numéricos da linha/coluna
loc -> nomes verdadeiras da linha/coluna


>>>> Fazer buscas no DataFrame
# Buscar quando coluna CodAmostra é "S-01_0,3" E coluna CodPrm é "P125"
print(df.query('CodAmostra == "S-01_0,3" & CodPrm == "P125"'))


>>>>  Inserir linhas (pode ser aprimorado utilizando concatenar ao invés de adicionar linha a DataFrame existente)

# Função para inserir nova linha em DataFrame
def inserir_linha_(numero_linha, df, novo_valor):
    if numero_linha > df.index.max() + 1:
        print("Numero_linha inválido!")
    else:
        # Fatia a parte superior do DataFrame
        df1 = df[0:numero_linha]

        # Armazena a parte inferior do DataFrame
        df2 = df[numero_linha:]

        # Insere nova linha na parte superior do DataFrame
        df1.loc[numero_linha] = novo_valor

        # Concatena os dois DataFrames
        df_result = pd.concat([df1, df2])

        # Atribui os rótulos dos índices
        df_result.index = [*range(df_result.shape[0])]

        # Retorna o DataFrame atualizado
        return df_result


# How to assign value (avoid SettingWithCopyWarning)
In general, you should use loc for label-based assignment, and iloc for integer/positional based assignment, as the spec guarantees that they always operate on the original. Additionally, for setting a single cell, you should use at and iat.
(Source)[https://stackoverflow.com/questions/20625582/how-to-deal-with-settingwithcopywarning-in-pandas]