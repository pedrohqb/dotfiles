# dotfiles

Trata-se de arquivos ocultos ("dotfiles") utilizados para configuração de workstation para exercício da advocacia no Brasil utilizando Linux. Tais arquivos farão o seguinte:

a) configurar a fonte Calibri, padrão de mercado para e-mails e petições, desativando a fontes de bitmap incorporadas (veja https://wiki.archlinux.org/title/Font_configuration);

b) configurar a fonte Calibri acima mencionada como a fonte utilizada pelo Evolution, o mais completo gerenciador de e-mails para Linux, seja ele instalado enquanto Flatpak ou pacote nativo da distribuição utilizada (rpm ou deb, por exemplo);

c) configurar o plugin utilizado pelo certificado digital do eSAJ via Firefox (Lacuna Web PKI e Softplan Web Signer) sem a necessidade de instalar os pacotes deb ou rpm fornecidos;

d) configurar o módulo de token Safesign, fornecido pela OAB-SP, nas configurações de pk11-kit, a fim de que possa ser utilizado de forma geral pelo sistema, inclusive em diversos navegadores;

e) desabilitar o módulo opensc, que em geral acompanha a instalação padrão do Fedora, uma vez que gera incompatibilidades com o certificado digital Safesign.

Tais configurações foram testadas no Debian 12, Arch (final de 2024) e Fedora Silverblue 41.

OBS 1: Os arquivos fazem referência ao meu usuário "pedro"; sua utilização dependerá da adaptação para o nome do usuário que irá utilizá-lo.

OBS 2: Para o módulo token Safesign funcionar com essas configurações, o arquivo libaetpkss.so e seus links simbólicos deverão ser extraídos do pacote deb e rpm e copiados para ~/.local/lib. Os pacotes podem ser encontrados aqui: https://certificaat.kpn.com/installatie-en-gebruik/installatie/pas-usb-stick/linux/. Minha experiência indica que as libs do pacote deb têm melhor compatibilidade entre distribuições.

OBS 3: Para os plugins utilizados pelo eSAJ (Lacuna Web PKI e Softplan Web Signer) funcionarem, será necessário baixar os pacotes deb de referidos plugins, extraí-los e copiar o executável webpki para ~/.lacuna-webpki e websigner para ~/.softplan-websigner. Eles podem ser baixados em https://get.webpkiplugin.com/ e https://websigner.softplan.com.br/.

---

Tutorial para extrair as libs do Safesign:

a) Faça o download do pacote do pacote deb para última versão do Ubuntu disponível em https://certificaat.kpn.com/installatie-en-gebruik/installatie/pas-usb-stick/linux/

b) Extraia o conteúdo do pacote deb rodando o seguinte comando no terminal: $ ar x nome-do-pacote.deb .

c) Extraia o conteúdo do pacote data.tar.zst, que irá aparecer após o rodando o comando acima, com o seguinte comando: $ tar --zstd -xvf data.tar.zst .

d) Crie o diretório lib em ~/.local/lib usando o seguinte comando: $ mkdir -p ~/.local/lib

e) Copie as libs necessários para ~/.local/lib usando o seguinte comando: $ cp usr/lib/libaetpkss.so* ~/.local/lib

---

Tutorial para extrair Lacuna Web PKI:

a) Instale o plugin para Firefox no respectivo site: https://get.webpkiplugin.com/ .

b) Extraia o conteúdo do pacote deb rodando o seguinte comando no terminal: $ ar x nome-do-pacote.deb .

c) Extraia o conteúdo do pacote data.tar.zst, que irá aparecer após o rodando o comando acima, com o seguinte comando: $ tar --zstd -xvf data.tar.zst .

d) Crie os diretórios rodando o seguinte comando: $ mkdir ~/.lacuna-webpki

e) Copie o executável webpki para seu diretório com o seguinte comando: $ cp opt/lacuna-webpki/webpki ~/.lacuna-webpki

---

Tutorial para extrair Softplan Web Signer:

a) Instale o plugin para Firefox no respectivo site: https://websigner.softplan.com.br/

b) Extraia o conteúdo do pacote deb rodando o seguinte comando no terminal: $ ar x nome-do-pacote.deb .

c) Extraia o conteúdo do pacote data.tar.zst, que irá aparecer após o rodando o comando acima, com o seguinte comando: $ tar xvf data.tar.xz .

d) Crie os diretórios rodando o seguinte comando: $ mkdir ~/.softplan-websigner

e) Copie o executável websigner para seu diretório com o seguinte comando: $ cp opt/softplan-websigner/websigner ~/.lacuna-webpki
