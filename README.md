# Resumo sobre instâncias EC2 

## Gerenciamento de EC2 e AMIs com AWS Toolkit for Visual Studio

&emsp;O AWS Toolkit for Visual Studio permite o gerenciamento de instâncias Amazon EC2 e Amazon Machine Images (AMIs) diretamente no ambiente de desenvolvimento do Visual Studio. Todas as operações são executadas no escopo da região especificada no AWS Explorer.   

## Visualizando AMIs e Instâncias EC2

&emsp;O AWS Explorer é o ponto central para a visualização e gestão de recursos.   

- **Acesso à Visualização**: Para visualizar AMIs ou Instâncias EC2, expanda o nó Amazon EC2 no AWS Explorer e clique duas vezes nos subnós AMIs ou Instâncias, ou use o menu de contexto (clique com o botão direito do mouse) e escolha Exibir.   
- **Configuração da Visualização**:
  - As colunas podem ser reordenadas por arrasto e classificadas por clique no cabeçalho.   
  - As visualizações podem ser configuradas usando listas suspensas, a caixa de filtro em **Viewing (Exibição)** e o menu **Show/Hide (Mostrar/ocultar)**.   
  - As configurações de coluna persistem ao reabrir a visualização.   
- **Exibição Inicial de AMIs**: Inicialmente, são exibidas AMIs de qualquer tipo de plataforma (Windows ou Linux) pertencentes à conta especificada no AWS Explorer.   

## Marcação de Recursos (Tagging)

&emsp;Tags (etiquetas) são pares de nome e valor que permitem anexar metadados a AMIs, instâncias e volumes.   

- **Aplicação de Tags**: É possível adicionar tags usando a lista suspensa **Show/Hide (Mostrar/Ocultar)**.   
- **Criação de Tags**:
  1. Digite um nome na caixa **Add (Adicionar)** e escolha o botão verde (+).   
  2. Selecione **Apply (Aplicar)**. A nova tag aparece em itálico como uma nova coluna.   
  3. Clique duas vezes na célula da coluna da tag para adicionar um valor.   
- **Comportamento de Tags**:
  - Tags com valores associados são preservadas se a coluna for ocultada.   
  - Tags sem valores associados são excluídas completamente pelo AWS Toolkit se desmarcadas.   
  - Os nomes das tags não diferenciam maiúsculas de minúsculas, mas são exclusivos por tipo de recurso (AMIs vs. Instâncias).   
- **Restrições Gerais de Tag**: O número máximo de tags por recurso é 50. O prefixo `aws:` é reservado para uso da AWS.   

## Criação e Lançamento de Instâncias EC2

&emsp;O Toolkit permite lançar instâncias EC2 a partir de AMIs e criar AMIs a partir de instâncias existentes.   

1. **Lançamento de uma Instância (Exemplo Windows Server):**
- Na visualização **AMIs**, filtre e selecione uma AMI.   
- Abra o menu de contexto e escolha **Launch Instance (Executar instância)**.   
- Na caixa de diálogo Launch New Amazon EC2 Instance, configure:
  - **Tipo de instância**: Escolha o tipo de instância EC2.   
  - **Nome**: Forneça um nome para a instância (máx. 256 caracteres).   
  - **Par de chaves**: Selecione ou crie um par de chaves para autenticação (necessário para login via RDP em Windows).   
  - **Grupo de segurança**: Escolha um grupo que permita o tráfego de entrada necessário (e.g., porta 3389 para RDP).   
  - **Perfil da instância**: Associa uma função do IAM à instância para definir permissões de aplicativo.   
2. **Criação de uma AMI a partir de uma Instância:**
  - No AWS Explorer, expanda **Amazon EC2** e selecione Instâncias.   
  - Clique com o botão direito na instância desejada e escolha **Create Image (ABS AMI)**.   
  - Na caixa de diálogo, adicione um nome e uma descrição para a nova imagem.   
  - Após a criação, a nova AMI pode ser visualizada na lista **AMIs** (pode ser necessário **Atualizar**).

## Conexão e Encerramento de Instâncias

&emsp;O Toolkit oferece opções para conectar e gerenciar o ciclo de vida das instâncias.   

- **Conexão (Windows Server)**:
  - Clique com o botão direito na instância e escolha **Abrir área de trabalho remota**.   
  - Selecione **Usar par de chaves EC2** para fazer login para autenticação RDP como administrador.   
- **Encerrando Instâncias**: Você pode Parar ou Encerrar instâncias em execução.   
  - **Parar**: Só é possível se a instância usar um volume Amazon EBS. Os dados no volume EBS são mantidos, mas a cobrança pelo armazenamento EBS continua.   
  - **Encerrar**: Se a instância não usar EBS, esta pode ser a única opção. Todos os dados no armazenamento da instância local serão perdidos. A cobrança pela instância EC2 é interrompida.   
  - Instâncias encerradas desaparecem da lista após um tempo.   
- **Comportamento de Desligamento do Windows**: É possível configurar se o desligamento do Windows deve resultar em Stop (Interromper) ou Terminate (Encerrar) a instância.   

## Gerenciamento de Grupos de Segurança

&emsp;Grupos de segurança atuam como firewalls e controlam o tráfego de rede de entrada para instâncias EC2.   

- **Criação**:
  1. No AWS Explorer, expanda **Amazon EC2 > Security Groups e escolha View (Exibir)**.   
  2. Na guia **EC2 Security Groups**, escolha **Create Security Group (Criar Grupo de Segurança)**.   
  3. Digite nome e descrição e clique em OK.   
- **Adição de Permissões**:
  - Selecione o grupo e escolha **Add Permission (Adicionar Permissão)**.   
  - Defina o Protocolo, **Porta e Rede** (ex: HTTP, HTTPS, RDP).   
  - O **Source CIDR** padrão `(0.0.0.0/0)` aceita tráfego de qualquer IP externo.   

