package CertificadoReaD;
import java.io.Console;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.security.KeyStore;
import java.security.cert.Certificate;

public class LeitorCertificadoPFXValidacaoSenha {

    public static void main(String[] args) {
        Console console = System.console();
        if (console == null) {
            System.out.println("Não foi possível obter o Console.");
            return;
        }

        // Caminho para o arquivo .pfx
        String caminhoCertificado = "caminho/para/seu/certificado.pfx";

        boolean carregadoComSucesso = false;
        do {
            // Solicita a senha do certificado ao usuário
            char[] senha = console.readPassword("Digite a senha do certificado: ");

            try {
                Certificate certificado = carregarCertificado(caminhoCertificado, senha);
                // Limpar a senha da memória por segurança
                java.util.Arrays.fill(senha, ' ');

                // Faz algo com o certificado
                System.out.println("Certificado carregado com sucesso.");
                carregadoComSucesso = true;
            } catch (FileNotFoundException e) {
                System.out.println("Arquivo do certificado não encontrado: " + caminhoCertificado);
                break; // Sair do loop se o arquivo não puder ser encontrado
            } catch (IOException e) {
                // Limpar a senha da memória por segurança
                java.util.Arrays.fill(senha, ' ');
                System.out.println("Senha incorreta. Tente novamente.");
            } catch (Exception e) {
                // Limpar a senha da memória por segurança
                java.util.Arrays.fill(senha, ' ');
                e.printStackTrace();
                break; // Sair do loop para outros tipos de erros
            }
        } while (!carregadoComSucesso);
    }

    private static Certificate carregarCertificado(String caminhoCertificado, char[] senha)
            throws Exception {
        KeyStore keyStore = KeyStore.getInstance("PKCS12");

        try (FileInputStream fis = new FileInputStream(caminhoCertificado)) {
            keyStore.load(fis, senha);
        }

        String alias = keyStore.aliases().nextElement();
        return keyStore.getCertificate(alias);
    }
}