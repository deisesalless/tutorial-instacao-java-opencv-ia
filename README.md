# Configuração do Ubuntu 22.04 com JDK 21 e OpenCV 4.10.0 no IntelliJ IDEA

Este tutorial ensina como configurar o Ubuntu 22.04 para usar o OpenCV 4.10.0 com Java JDK 21 no IntelliJ IDEA.

## Passo a Passo

### 1. Instalar o JDK 21 e Ant
Instale o JDK 21 e o Ant, essenciais para o processo de instalação do OpenCV:
```bash
sudo apt install openjdk-21-jdk ant
```

### 2. Instalar o CMake
Instale o CMake para configurar o ambiente de construção do OpenCV:
```bash
sudo apt install cmake
```

### 3. Criar Pasta de Instalação
Crie uma pasta na localização de sua preferência para armazenar os arquivos do OpenCV. Por exemplo:
```bash
mkdir instalacao_opencv
cd instalacao_opencv
```

### 4. Clonar o Repositório do OpenCV
Faça o clone do repositório oficial do OpenCV na pasta criada anteriormente. Aqui usamos a versão 4.10.0:
```bash
git clone https://github.com/opencv/opencv/tree/4.10.0
cd opencv
```

### 5. Criar a Pasta build
Dentro da pasta **opencv**, crie uma pasta chamada build:
```bash
mkdir build
cd build
```

### 6. Configurar a Construção com o CMake
Execute o seguinte comando dentro da pasta **build**. Caso algum erro ocorra nos passos 6 a 9, apague a pasta build e reinicie o processo.
```bash
cmake -D CMAKE_BUILD_TYPE=Release \
      -D CMAKE_INSTALL_PREFIX=/usr/local \
      -D BUILD_JAVA=ON ..
```

### 7. Compilar o OpenCV
Compile o OpenCV com o comando:
```bash
make -j$(nproc)
```

### 9. Localizar os Arquivos Gerados
Após a instalação, o terminal mostrará a localização dos arquivos **libopencv_java4100.so** e **opencv-4100.jar**. Eles devem estar em:
```bash
/usr/local/share/java/opencv4/libopencv_java4100.so
/usr/local/share/java/opencv4/opencv-4100.jar
```

### 10.  Atualizar o Cache do Linker
Execute o comando abaixo para atualizar o cache do linker:
```bash
sudo ldconfig
```

## Configuração no IntelliJ IDEA

### 11.  Criar o Projeto
Crie um novo projeto no IntelliJ IDEA utilizando o JDK 21.

### 12.  Adicionar o JAR do OpenCV
Adicione o arquivo *opencv-4100.jar* ao seu projeto:

1. Acesse File > Project Structure > Modules > Dependencies.
2. Clique em + e selecione JARs or Directories.
3. Navegue até a localização do arquivo */usr/local/share/java/opencv4/opencv-4100.jar.*
4. Se precisar de mais detalhes, consulte este tutorial em vídeo: [Configuração do OpenCV no IntelliJ IDEA.](https://www.youtube.com/watch?v=TsUhEuySano)

**Obs.: O passo 3 pode mudar caso o seu resultado tenha sido diferente no passo 9.**

## Testando a Configuração
No método *main* do seu projeto, adicione as linhas abaixo:

```bash
import org.opencv.core.Core;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class ImageAIApplication {

	public static void main(String[] args) {
		SpringApplication.run(ImageAIApplication.class, args);
		System.loadLibrary(Core.NATIVE_LIBRARY_NAME);
		System.out.println(Core.VERSION);
	}

}
```

### Resultado Esperado
Ao executar o projeto, o console deve exibir:
```bash
4.10.0-dev
```
Se este for o resultado, a configuração foi realizada com sucesso! 🎉

