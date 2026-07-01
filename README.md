# SkillUpPlus 2030+

## Descrição do Projeto

O **SkillUpPlus 2030+** é um aplicativo móvel desenvolvido em **React Native** (utilizando **Expo Router**) para apoiar trabalhadores e estudantes na requalificação profissional frente às transformações do mercado, inspirando-se nos ODS 4 (Educação de Qualidade) e ODS 8 (Trabalho Decente e Crescimento Econômico).

O aplicativo implementa uma **estrutura de navegação híbrida** (Stack, Drawer e Tab Navigation) e utiliza componentes nativos do React Native, Hooks e persistência de dados (AsyncStorage) para simular o login e salvar informações do usuário.


## Estrutura de Navegação

1.  **Stack Navigation (Fluxo Sequencial):**
    *   `index.tsx` (Tela de Login/Boas-vindas) -> `(drawer)` (Tela Principal)

2.  **Drawer Navigation (Menu Lateral):**
    *   Agrupa as principais seções do aplicativo:
        *   `(tabs)`: Grupo de navegação principal (Home, Autoavaliação, Trilhas, Progresso).
        *   `profile`: Tela de Perfil.
        *   `settings`: Tela de Configurações.

3.  **Tab Navigation (Abas Inferiores):**
    *   Agrupa as funcionalidades centrais do aplicativo:
        *   `home`: Tela Inicial.
        *   `assessment`: Tela de Autoavaliação (com formulário e Picker).
        *   `trilhas`: Tela de Trilhas de Aprendizado (com ScrollView).
        *   `progress`: Tela de Monitoramento de Progresso.

## Tecnologias Utilizadas

*   **Framework:** React Native (com Expo)
*   **Roteamento:** Expo Router
*   **Navegação:** `@react-navigation/drawer`, `@react-navigation/bottom-tabs`, `@react-navigation/stack`
*   **Persistência de Dados:** `@react-native-async-storage/async-storage`
*   **Componentes:** `View`, `ScrollView`, `TextInput`, `Text`, `Button`, `Image`, `StyleSheet`, `TouchableOpacity`, `Alert`, `Picker`.


## Ambiente de Desenvolvimento
O aplicativo SkillUpPlus 2030+ teve sua lógica de negócios, estrutura de navegação híbrida (Stack, Drawer e Tabs) e persistência de dados validados com sucesso na plataforma Web, conforme evidenciado nas capturas de tela apresentadas no relatório. O funcionamento na Web comprova a integridade do código JavaScript/TypeScript e a correta implementação dos componentes do React Native e Expo Router.

No entanto, durante os testes em ambiente nativo simulado (Emulador Android - Pixel 5 / API 33), identificou-se uma limitação técnica relacionada ao ambiente de execução do Expo Go.

Diagnóstico do Problema: Na primeira execução do aplicativo foi detectada uma inconsistência crítica de versões na biblioteca react-native-reanimated (dependência essencial para o Drawer Navigator), gerando o erro "Worklets Mismatch". 

Este erro ocorre devido a um descompasso entre a versão da biblioteca JavaScript instalada no projeto (v0.6.1) e a versão do binário nativo pré-compilado presente no aplicativo Expo Go do emulador (v0.5.1).


ERROR  [WorkletsError: [Worklets] Mismatch between JavaScript part and native part of Worklets (0.6.1 vs 0.5.1).
    See `https://docs.swmansion.com/react-native-worklets/docs/guides/troubleshooting#mismatch-between-javascript-part-and-native-part-of-worklets` for more details.]


Comportamento da Aplicação: É importante ressaltar que este erro não bloqueia a lógica da aplicação. Ao interagir com a interface de depuração do Expo Go e selecionar as opções "Minimize" ou "Dismiss", o erro é ocultado e é possível prosseguir com a navegação normalmente entre as telas de Login, Home, Trilhas e Perfil. Isso corrobora que a estrutura de rotas e a lógica de negócios estão funcionais, sendo a falha isolada exclusivamente na camada de animação nativa do Drawer.

## Estrutura de Diretórios

```
SkillUpPlus2030Plus/
├── app/
│   ├── (drawer)/
│   │   ├── (tabs)/
│   │   │   ├── _layout.tsx         # Layout da Tab Navigation
│   │   │   ├── home.tsx            # Tela Home
│   │   │   ├── assessment.tsx      # Tela de Autoavaliação (Formulário/Picker)
│   │   │   ├── trilhas.tsx         # Tela de Trilhas (ScrollView)
│   │   │   └── progress.tsx        # Tela de Progresso
│   │   ├── _layout.tsx             # Layout da Drawer Navigation
│   │   ├── profile.tsx             # Tela de Perfil
│   │   └── settings.tsx            # Tela de Configurações
│   ├── _layout.tsx                 # Layout da Stack Navigation (Root)
│   └── index.tsx                   # Tela de Login/Inicial
├── assets/
├── babel.config.js
├── app.json
├── package.json
└── README.md
```

## Como Executar o Projeto

Para configurar e executar o projeto, siga os passos abaixo:

1.  **Instale as dependências:**

    ```bash
    npm install
    ```

2.  **Limpe e Execute o projeto (Modo Seguro):**
    É fundamental iniciar o Metro Bundler com o *flag* `--clear` para garantir que o cache de compilação seja limpo e que o aplicativo carregue a versão correta das bibliotecas nativas (`react-native-reanimated`).

    ```bash
    npx expo start --clear
    ```

3.  **Acesso ao Aplicativo:**

      * **Emulador/Dispositivo:** Use o aplicativo **Expo Go** no seu celular ou um emulador Android/iOS para escanear o QR Code exibido no terminal.
      * **Web:** Pressione `w` no terminal para abrir o projeto no navegador (Web).

-----

### Observação Adicional

> **⚠️ Nota sobre o ambiente Android:**
>
> Se, ao iniciar o projeto no Android, ocorrer o erro **`Worklets Mismatch`**, trata-se de um conflito de cache do aplicativo **Expo Go** no seu dispositivo. Para resolver, desinstale e reinstale o aplicativo Expo Go no seu emulador/celular, ou limpe o cache nativo dele (Configurações \> Apps \> Expo Go \> Armazenamento \> Limpar Dados/Cache).
