# 📊 Power BI - Modelagem de Dados | Portfolio

Projeto completo de **Modelagem de Dados** no Power BI, demonstrando boas práticas de modelagem dimensional (Star Schema), relacionamentos, medidas DAX e documentação técnica.

> Projeto desenvolvido como parte de estudos e práticas em Business Intelligence e Analytics.

---

## 🎯 Sobre o Projeto

Este repositório apresenta um modelo de dados robusto construído no Power BI Desktop, utilizando dados de vendas, clientes, produtos, revendedores, territórios e estoque.

### Principais objetivos:
- Criar um **modelo estrela (Star Schema)** limpo e performático
- Implementar relacionamentos ativos e inativos
- Utilizar `USERELATIONSHIP` para análises com múltiplas datas
- Gerar medidas de negócio (Total de Pedidos e Total de Entregas)
- Documentar todo o modelo de forma profissional

---

## 🗂️ Estrutura do Modelo

### Tabelas de Dimensão
| Tabela | Descrição |
|--------|-----------|
| **Cliente** | Dados dos clientes (nome, cidade, estado, país, CEP) |
| **Produto** | Catálogo de produtos (SKU, nome, custo, preço, cor, modelo, categoria e subcategoria) |
| **Revendedor** | Informações dos revendedores e tipo de negócio |
| **VendasTerritorio** | Região, país e continente |
| **Calendario** | Tabela de datas gerada (2017 a 2022) com chave `DataKey` |

### Tabelas de Fato
| Tabela | Descrição |
|--------|-----------|
| **Vendas** | Fato principal (quantidade, preço unitário, custo, datas de pedido, vencimento e entrega) |
| **Estoque** | Quantidade de estoque por produto e data de atualização |

### Tabela de Medidas
- Tabela dedicada `Medidas` para organização das medidas DAX.

---

## 🔗 Relacionamentos

| De | Para | Tipo | Ativo |
|----|------|------|-------|
| Vendas[ClienteKey] | Cliente[ClienteKey] | Muitos para Um | ✅ |
| Vendas[ProdutoKey] | Produto[ProdutoKey] | Muitos para Um | ✅ |
| Vendas[RevendedorKey] | Revendedor[RevendedorKey] | Muitos para Um | ✅ |
| Vendas[VendasTerritorioKey] | VendasTerritorio[VendasTerritorioKey] | Muitos para Um | ✅ |
| Vendas[PedidoVendaDataKey] | Calendario[DataKey] | Muitos para Um | ✅ (ativo) |
| Vendas[EntregaDataKey] | Calendario[DataKey] | Muitos para Um | ❌ (inativo) |
| Vendas[VencimentoDataKey] | Calendario[DataKey] | Muitos para Um | ❌ (inativo) |
| Estoque[ProdutoKey] | Produto[ProdutoKey] | Muitos para Um | ✅ |
| Estoque[Data atualização] | Calendario[Date] | Muitos para Um | ✅ |

---

## 📈 Medidas DAX

### Total pedidos
```dax
Total pedidos = 
CALCULATE(
    COUNTROWS(Vendas),
    USERELATIONSHIP(Calendario[DataKey], Vendas[PedidoVendaDataKey])
)
```

### Total entregas
```dax
Total entregas = 
CALCULATE(
    COUNTROWS(Vendas),
    USERELATIONSHIP(Calendario[DataKey], Vendas[EntregaDataKey])
)
```

Essas medidas permitem analisar pedidos e entregas independentemente, utilizando relacionamentos inativos com a tabela de calendário.

---

## 🛠️ Técnicas Utilizadas

- **Power Query**: Limpeza e transformação de dados (remoção de barras em datas, renomeação de colunas, joins)
- **Modelo Dimensional**: Star Schema
- **Relacionamentos Múltiplos com Datas**: Uso de `USERELATIONSHIP`
- **Tabela Calendário** gerada via DAX
- **Documentação completa** do modelo (gerada com Power BI Helper)

---

## 📁 Arquivos do Repositório

| Arquivo | Descrição |
|---------|-----------|
| `README.md` | Esta documentação |
| `docs/PowerBI-ModelagemDeDados-ProjetoFinal-Documentacao.htm` | Documentação técnica completa do modelo |
| `data/Estoque - Power BI Modelagem de dados.xlsx` | Dados de estoque |

> **Nota**: Os arquivos maiores (`Base de dados - Power BI Modelagem de dados.xlsx` e o arquivo `.pbix`) não foram incluídos diretamente no repositório devido ao limite de tamanho. Eles podem ser solicitados ou adicionados via Git LFS se necessário.

---

## 🚀 Como usar

1. Clone o repositório
2. Abra o arquivo `.pbix` no Power BI Desktop (se disponível)
3. Explore o modelo de dados, relacionamentos e medidas
4. Utilize a documentação HTML para entender a estrutura completa

---

## 🧑‍💻 Autor

**Marcos Monteiro**  
📍 Espírito Santo, Brasil  
🔗 [GitHub](https://github.com/Marcosmto)

---

## 📄 Licença

Este projeto é de uso educacional e de portfólio.
