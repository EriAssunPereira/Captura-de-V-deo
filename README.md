# Captura de Vídeo em Aplicativos React Native

## Introdução
A captura de vídeo é uma funcionalidade essencial em muitos aplicativos móveis, e o React Native oferece maneiras de integrar essa funcionalidade de forma eficiente. Neste artigo, vamos explorar como criar um aplicativo React Native que permite aos usuários gravar vídeos, salvar esses vídeos em seus álbuns e compartilhá-los com facilidade.

## Pré-requisitos
Antes de começarmos, certifique-se de ter o seguinte instalado:

1. **Node.js e npm**: Vamos usar o Node.js para desenvolver nosso aplicativo.
2. **React Native CLI**: Instale o React Native Command Line Interface para criar e gerenciar projetos React Native.
3. **Expo CLI (opcional)**: O Expo é uma ferramenta que facilita o desenvolvimento React Native. Você pode instalá-lo globalmente com `npm install -g expo-cli`.

## Passo 1: Configuração do Projeto
Crie um novo projeto React Native chamado "MeuApp". Dentro dele, crie os seguintes arquivos:

- `CameraScreen.js`: Esta tela conterá a lógica para capturar vídeos usando a câmera do dispositivo.
- `VideoPreviewScreen.js`: Aqui, os usuários poderão visualizar o vídeo gravado antes de salvá-lo.
- `VideoListScreen.js`: Uma lista de todos os vídeos gravados pelos usuários.
- `ShareScreen.js`: Tela para compartilhar os vídeos.

## Passo 2: Captura de Vídeo com Expo Camera
Vamos usar o pacote `expo-camera` para capturar vídeos. No arquivo `CameraScreen.js`, configure a câmera e adicione os botões para iniciar e parar a gravação:

```javascript
// CameraScreen.js
import React, { useState, useRef } from 'react';
import { View, Text, TouchableOpacity } from 'react-native';
import { Camera } from 'expo-camera';

const CameraScreen = () => {
  const cameraRef = useRef(null);
  const [isRecording, setIsRecording] = useState(false);

  const startRecording = async () => {
    if (cameraRef.current) {
      await cameraRef.current.recordAsync();
      setIsRecording(true);
    }
  };

  const stopRecording = async () => {
    if (cameraRef.current && isRecording) {
      const video = await cameraRef.current.stopRecording();
      // Salve o vídeo ou faça outras ações
      setIsRecording(false);
    }
  };

  return (
    <View>
      <Camera ref={cameraRef} style={{ flex: 1 }} type={Camera.Constants.Type.back} />
      <TouchableOpacity onPress={isRecording ? stopRecording : startRecording}>
        <Text>{isRecording ? 'Parar' : 'Gravar'}</Text>
      </TouchableOpacity>
    </View>
  );
};

export default CameraScreen;
```

## Passo 3: Visualização e Compartilhamento
Na tela `VideoPreviewScreen.js`, mostre o vídeo gravado e adicione opções para salvar e compartilhar. Na tela `VideoListScreen.js`, liste todos os vídeos gravados pelos usuários.

## Conclusão
Parabéns! Você criou um aplicativo de captura de vídeo em React Native. Personalize-o, adicione mais recursos e torne-o ainda mais incrível!
