# Player Plugin

Plugin Capoeira Music para execução dos áudios do projeto. A interface do usuário (UI) é construída com Flutter, enquanto a lógica de reprodução de áudio é implementada nativamente em Kotlin (usando ExoPlayer) e Swift (usando AVPlayer).

## Arquitetura

Este plugin utiliza a abordagem de Platform Channels:

- **Interface (Flutter):** Uma UI customizável e de alta performance, escrita uma única vez em Dart.
- **Funcionalidade (Nativo):** Acesso direto às APIs de áudio de cada plataforma (ExoPlayer/AVPlayer), permitindo funcionalidades como reprodução em segundo plano, controles na tela de bloqueio e gerenciamento de interrupções.

## Funcionalidades

- [ ] Reprodução de arquivos locais (MP3).
- [ ] Reprodução de áudio via streaming (HTTP).
- [ ] Controles básicos: `play`, `pause`, `stop`, `seek`.
- [ ] Notificação de status do player (`playing`, `paused`, `completed`, `error`).
- [ ] Acompanhamento do progresso da reprodução.
- [ ] Reprodução em segundo plano (background audio).
- [ ] Controles na tela de bloqueio e na central de notificações.

## Instalação

Incluir ao `pubspec.yaml` do projeto principal:

```yaml
dependencies:
  player: ^0.0.1
```

E execute `flutter pub get`.

## Configuração

### Android

Adicione as permissões necessárias ao seu `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.INTERNET" />
<!-- Adicione outras permissões se for tocar áudio em segundo plano -->
```

### iOS

Adicione as chaves necessárias ao seu `Info.plist`:

```xml
<key>UIBackgroundModes</key>
<array>
    <string>audio</string>
</array>
```

## Como Usar

O uso do player no app principal ainda será alinhado:

```dart
import 'package:flutter/material.dart';
import 'package:player/player.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  final _player = Player();
  String? _platformVersion;

  @override
  void initState() {
    super.initState();
    // Exemplo de como obter a versão da plataforma
    _player.getPlatformVersion().then((version) {
      setState(() {
        _platformVersion = version;
      });
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Player Plugin Exemplo'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text('Versão da Plataforma: $_platformVersion\n'),
              ElevatedButton(
                onPressed: () {
                  // TODO: Implementar chamada de play
                  // _player.play('URL_DO_AUDIO');
                },
                child: Text('Play'),
              ),
              ElevatedButton(
                onPressed: () {
                  // TODO: Implementar chamada de pause
                  // _player.pause();
                },
                child: Text('Pause'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```
