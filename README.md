# Atividade-criptografia

Módulo 1: Introdução, Conceitos Fundamentais e a Matemática por Trás do Segredo
1. O que é Criptografia RSA?
A Criptografia RSA (Rivest-Shamir-Adleman) é um algoritmo de criptografia assimétrica (ou de chave pública) desenvolvido em 1977.
• Princípio Básico: O RSA resolve um problema fundamental da criptografia: como enviar uma mensagem codificada a alguém sem compartilhar previamente o código.
• Nome: Recebeu o nome de seus criadores: o matemático e os dois cientistas da computação.
• Bidirecionalidade: Pode ser usado tanto para criptografia quanto para assinatura digital.


2. Criptografia Assimétrica (Chave Pública)
O RSA é o algoritmo de chave pública mais usado no mundo.

Caracteristica - Chave publica
Criptografar dados (qualquer um pode enviar a mensagem)
Chave privada - Descriptografar dados (somente o destinatário pode ler)
Status - Chave publica
Bem conhecida e compartilhada abertamente
Chave privada - Secreta e disponível apenas ao seu proprietário
Componentes - Chave publica
Módulo (n) e Expoente Público (e)
Chave privada - Módulo (n) e Expoente Privado (d)
Assinatura - Chave publica
Chave privada - Verifica a assinatura digital
Gera a assinatura digital
Em contraste, a Criptografia Simétrica (como AES) usa a mesma chave para criptografar e descriptografar.


3. A Matemática no Núcleo do RSA
A segurança do RSA depende inteiramente de conceitos complexos da teoria dos números.
A. Funções de Porta de Armadilha (Trapdoor Functions)
O RSA é baseado em equações que são simples de calcular em uma direção e extremamente difíceis na direção inversa.
• O Problema da Fatoração: O RSA utiliza o fato de que é fácil multiplicar dois números primos grandes (p×q=n), mas é computacionalmente difícil reverter a operação, ou seja, descobrir os fatores p e q dado apenas n.
B. Aritmética Modular
É a matemática do resto e é fundamental para o funcionamento eficiente do RSA.
• Módulo (n): A operação amodn significa o restante deixado após a divisão de a por n.
• Exponenciação Modular: O algoritmo Square-and-Multiply é usado para calcular potências grandes eficientemente (a 
k
 modn) e é crucial para viabilizar o RSA.
C. Totiente de Euler (φ(n)) e Inverso Modular
• Função Totiente: Para o produto de dois primos distintos (n=p×q), a função φ(n) é calculada como φ(n)=(p−1)×(q−1).
• Teorema de Euler: Este teorema garante a reversibilidade do processo, provando que a mensagem descriptografada retorna à original.
• Inverso Modular (d): O expoente privado d é o inverso modular de e módulo φ(n), calculado tal que e×d≡1(modφ(n)). Isso é feito usando o Algoritmo Euclidiano Estendido.

--------------------------------------------------------------------------------
Módulo 2: O Fluxo do Algoritmo e Uso Prático
4. Geração de Chaves (Alicerces do Segredo)
Esta é a primeira fase do RSA, onde o destinatário (ex: Alice) cria seu par de chaves.

1. Passo - Gerar Primos (p,q)

Componente - Escolher dois primos grandes e distintos, p e q.

Ação - Para uma chave de n bits, p e q devem ter aproximadamente n/2 bits cada.
2. Passo - Calcular Módulo (n)

Ação - n=p×q.

Componente - Módulo Público (n). Define o tamanho da chave.
3. Passo - Calcular Totiente (φ(n))

Ação - φ(n)=(p−1)×(q−1).

Componente - Mantido em segredo.
4. Passo - Escolher Expoente Público (e)

Açao - Escolher e coprimo com φ(n).

Componente - Um valor comum é e=65537, pois tem poucos bits '1' em binário, facilitando a exponenciação.
5. Passo - Calcular Expoente Privado (d)

Ação - d=e^−1 modφ(n).

Componente - Expoente Privado (d), calculado via Algoritmo Euclidiano Estendido.

5. Criptografia e Descriptografia
O RSA permite que a mensagem seja enviada de forma segura.

Criptografia
Ação - Conversão da mensagem (m) para o texto cifrado (c).

Formula - c=m^e mod n

Chave utilizada - Chave Pública (n,e)

Descriptografia
Açao - Recuperação do texto cifrado (c) para a mensagem original (m). 

Formula - m=c^d mod n

have utilizada - Chave Privada (n,d)

6. Uso Prático e Híbrido
O RSA não é eficiente para criptografar grandes volumes de dados.
• Lentidão: O RSA é mais lento (aproximadamente 1000 vezes) do que algoritmos simétricos (como AES).
• Uso Híbrido Comum: A prática é usar o RSA para criptografar apenas a chave simétrica de sessão (ex: AES ou DES). Essa chave simétrica é então usada para criptografar os dados em massa, combinando a segurança do RSA com a velocidade do AES.
O RSA é amplamente usado em protocolos como SSL-TLS, SSH, VPNs e serviços de e-mail.

--------------------------------------------------------------------------------
Módulo 3: Segurança, Desafios e o Futuro
7. Segurança e Tamanhos de Chave
A segurança do RSA é proporcional ao tamanho de suas chaves.
• Recomendação Mínima: O NIST (Instituto Nacional de Padrões e Tecnologia) recomenda um comprimento mínimo de chave de 2048 bits (equivalente a 112 bits de segurança simétrica).
• Segurança Ampliada: Organizações estão adotando comprimentos de chave de 3072 bits ou 4096 bits para maior segurança.
• Vulnerabilidades por Chave Fraca: Chaves de 768 bits já foram quebradas. Se os primos p e q estiverem muito próximos ou se um dos números que compõem o par de chaves for muito pequeno, o algoritmo se torna mais fácil de resolver.

8. Desafios e Contramedidas
O RSA, embora robusto, não está isento de vulnerabilidades se implementado incorretamente.
• Ataques de Canal Lateral: Invasores podem extrair a chave privada analisando informações vazadas, como o consumo de energia ou o tempo de processamento da máquina durante a descriptografia.
    ◦ Contramedida: Implementar operações criptográficas em tempo constante para evitar vazamentos temporais.
• Ataques de Padding: Para evitar ataques que exploram a formatação da mensagem, é fundamental usar esquemas de preenchimento (padding) seguros.
    ◦ Contramedida: O padrão atual é o OAEP (Optimal Asymmetric Encryption Padding) para criptografia e PSS para assinatura digital.
    
9. O Futuro do RSA: A Ameaça Quântica
• Algoritmo de Shor: A computação quântica representa um desafio significativo, pois o Algoritmo de Shor (1994) pode resolver o problema da fatoração de inteiros em tempo polinomial.
• Vulnerabilidade: Visto que a segurança do RSA depende da dificuldade de fatoração, os computadores quânticos tornarão os tamanhos atuais de chave vulneráveis.
• Contramedida: A indústria está trabalhando ativamente na migração para a Criptografia Pós-Quântica (PQC), com algoritmos como Kyber e Dilithium (baseados em lattice) já sendo padronizados pelo NIST.

🛠️ Passo a passo: Criando e usando o código RSA em Rust

1️⃣ Instalar Rust

No terminal do Codespace, instale Rust se necessário

    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    source $HOME/.cargo/env

2️⃣ Criar um novo projeto Rust

    cargo new memoria_demo
    cd memoria_demo

3️⃣ Adicionar dependências no Cargo.toml

    [package]

    name = "memoria_demo"
    version = "0.1.0"
    edition = "2024"

    [dependencies]
    num-bigint = "0.4"
    num-traits = "0.2"

4️⃣ Criar o código RSA Substitua o conteúdo de src/main.rs por:

    use num_bigint::{BigUint, ToBigUint};
    use num_traits::{One, Zero};

    fn modular_inverse(a: &BigUint, m: &BigUint) -> BigUint {
    let (mut t, mut new_t) = (BigUint::zero(), BigUint::one());
    let (mut r, mut new_r) = (m.clone(), a.clone());

    while new_r != BigUint::zero() {
        let q = &r / &new_r;

        let temp_t = new_t.clone();
        new_t = if &t > &(&q * &new_t) {
            (&t - &q * &new_t) % m
        } else {
            (m - ((&q * &new_t) - &t) % m) % m
        };
        t = temp_t;

        let temp_r = new_r.clone();
        new_r = &r - &q * &new_r;
        r = temp_r;
    }

    t % m
    }

    fn modular_pow(base: &BigUint, exponent: &BigUint, modulus: &BigUint) -> BigUint {
    base.modpow(exponent, modulus)
    }

    fn generate_rsa_keys() -> ((BigUint, BigUint), (BigUint, BigUint)) {
    let p = 71u32.to_biguint().unwrap();
    let q = 67u32.to_biguint().unwrap();

    let n = &p * &q;
    let phi = (&p - 1u32) * (&q - 1u32);
    let e = 19u32.to_biguint().unwrap();
    let d = modular_inverse(&e, &phi);

    ((n.clone(), e), (n, d))
    }

    fn rsa_encrypt(message: &BigUint, public_key: &(BigUint, BigUint)) -> BigUint {
    let (n, e) = public_key;
    modular_pow(message, e, n)
    }

    fn rsa_decrypt(ciphertext: &BigUint, private_key: &(BigUint, BigUint)) -> BigUint {
    let (n, d) = private_key;
    modular_pow(ciphertext, d, n)
    }

    fn main() {
    let (public_key, private_key) = generate_rsa_keys();

    println!("==================== RSA DEMO ====================");
    println!(">>> Chave Pública  : (n = {}, e = {})", public_key.0, public_key.1);
    println!(">>> Chave Privada  : (n = {}, d = {})", private_key.0, private_key.1);
    println!("=================================================\n");

    let mensagem = 123u32.to_biguint().unwrap();
    println!("Mensagem Original: {}", mensagem);

    let cifrado = rsa_encrypt(&mensagem, &public_key);
    println!("Mensagem Criptografada: {}", cifrado);

    let decifrado = rsa_decrypt(&cifrado, &private_key);
    println!("Mensagem Decifrada   : {}", decifrado);

    println!("\n✅ Operação concluída com sucesso!");
    }

5️⃣ Executar o código

cargo run
Você verá a saída mostrando:

Chave pública e privada

Mensagem original

Mensagem criptografada

Mensagem descriptografada
