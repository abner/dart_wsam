# Instalação

1. Instalado a dependência wasm via referência ao repositório no github: https://github.com/dart-lang/wasm.git

2. Após rodar pub get, foi executado o comando `dart run wasm:setup`

3. No entanto o comando falhou, dando falta do arquivo .dart_tool/pub/bin/wasm/Cargo.toml

Observamos que alguns arquivos estavam faltando, então baixamos do repositório os arquivos da pasta [bin](https://github.com/dart-lang/wasm/tree/main/bin) e colamos
em .dart_tool/pub/bin/wasm/ e então o comando `dart run wasm:setup` funcionou.

Abrimos uma issue no repositório (dart-lang/wasm no github](https://github.com/dart-lang/wasm/issues/17).


4. Para a geração do square.wasm no Ubuntu, realizamos os seguintes passos:

  4.1 Instalação clang-12
     ```bash
     sudo apt-get install clang-12 ldd-12
     ```
  4.2 Criando alternative para wasm-ld apontando para wasm-ld-12
     ```bash
     sudo update-alternatives --install /usr/bin/wasm-ld wasm-ld /usr/bin/wasm-ld-12 100
     ```
  4.3 Compilação
    ```bash
    clang-12 --target=wasm32 -nostdlib -Wl,--export-all -Wl,--no-entry -o square.wasm square.cc
    ```
   