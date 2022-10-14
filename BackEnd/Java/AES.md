<h1> 1. AES 란? </h1>

> AES는 고급 암호화 표준이라는 의미이며, 암호화 및 복호화 시 동일한 키를 사용하는 대칭키 알고리즘
>
> AES의 종류는 AES-128, AES-192, AES-256이 있고 각각 뒤에 붙은 숫자가 키의 길이를 의미
>
> AES 암호화 알고리즘은 높은 안정성과 빠른 속도로 전세계적으로 사용되고 있다.
 

<h3> 2. AES 암호화 설명 </h3>

<h4> 1) Secret Key </h4>

> Secret Key는 평문을 암호화하는데 사용되며 절대로 외부에 노출되어서는 안된다.
> AES의 종류가 무엇이냐에 따라 Secret Key의 길이가 달라진다.
>
> (AES-256는 256비트(32바이트)의 키를 사용)
 

<h4> 2) Block Cipher </h4>

> AES는 128비트(16바이트)의 고정된 블록 단위로 암호화를 수행한다. (이는 암호화 키의 길이와 전혀 무관)
> 암호화를 수행할 때 여러가지 Block Cipher Mode를 선택할 수있으며 크게 CBC, ECB 등이 존재한다.
> 권장하는 방식은 CBC 방식이다.
>
> AES는 128비트의 블록단위로 암호화를 수행하는데 128비트보다 작은 블록이 생길 경우 부족한 부분을 특정 값으로 채워야한다.
> 이러한 작업을 **패딩**이라고 부르며, 대표적으로 PKCS5, PCKS7 방식이 있다.
 

<h4> 3) CBC (Ciper Block Chaning) </h4>

> AES는 128비트의 고정된 블록 단위로 암호화를 수행하는데, CBC는 블록을 그대로 암호화 하지않고 이전에 암호화했던 블록과 XOR 연산을 한 다음에 암호화를 수행한다.
> 
> 그래서 같은 내용을 갖는 원문 블록이라도 전혀다른 암호문을 갖게됩니다. 그런데 첫번째 블록은 이전 암호화 블록이 없기 때문에 이를 위해 IV(initialization vector)를 이용한다.
>
> AES는 128비트(16바이트)단위로 암호화 하기때문에 IV또한 16바이트 크기여야한다. 
> IV가 생성되면 이 값을 가지고 첫번째 블록을 암호화 한다. 매번 다른 IV를 생성하면 같은 평문이라도 다른 암호문을 생성할 수 있다.
 

<h3> 3. AES-256 예제 </h3>

``` java

import java.util.Base64;
import javax.crypto.Cipher;
import javax.crypto.spec.IvParameterSpec;
import javax.crypto.spec.SecretKeySpec;

public class AES256 {

    public static String alg = "AES/CBC/PKCS5Padding";
    private final String key = "01234567890123456789012345678901";
    private final String iv = key.substring(0, 16); // 16byte

    public String encrypt(String text) throws Exception {
        Cipher cipher = Cipher.getInstance(alg);
        SecretKeySpec keySpec = new SecretKeySpec(key.getBytes(), "AES");
        IvParameterSpec ivParamSpec = new IvParameterSpec(iv.getBytes());
        cipher.init(Cipher.ENCRYPT_MODE, keySpec, ivParamSpec);

        byte[] encrypted = cipher.doFinal(text.getBytes("UTF-8"));
        return Base64.getEncoder().encodeToString(encrypted);
    }

    public String decrypt(String cipherText) throws Exception {
        Cipher cipher = Cipher.getInstance(alg);
        SecretKeySpec keySpec = new SecretKeySpec(key.getBytes(), "AES");
        IvParameterSpec ivParamSpec = new IvParameterSpec(iv.getBytes());
        cipher.init(Cipher.DECRYPT_MODE, keySpec, ivParamSpec);

        byte[] decodedBytes = Base64.getDecoder().decode(cipherText);
        byte[] decrypted = cipher.doFinal(decodedBytes);
        return new String(decrypted, "UTF-8");
    }

}

public class Main {

    public static void main(String[] args) throws Exception {

        AES256 aes256 = new AES256();
        String text = "!! Hello World !!";
        String cipherText = aes256.encrypt(text);
        System.out.println(text);
        System.out.println(cipherText);
        System.out.println(aes256.decrypt(cipherText));
    }
}

```

출처 : https://bamdule.tistory.com/234 - [ [JAVA] AES-256 암호화 하기 ]
