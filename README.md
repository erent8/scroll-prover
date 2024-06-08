# 📜 scroll-prover 📜
[![Unit Test](https://github.com/scroll-tech/scroll-prover/actions/workflows/unit_test.yml/badge.svg)](https://github.com/scroll-tech/scroll-prover/actions/workflows/unit_test.yml)
![issues](https://img.shields.io/github/issues/scroll-tech/scroll-prover)

## Kullanım

### En son sürüm
v0.10.3 sürümü şu anda Scroll Mainnet'te kullanılmaktadır. main dalının en son hali ise geliştirme için kullanılmaktadır

### Önkoşul
Solidity derleyicisi `solc` sürümünün `0.8.19` sürümünü yükleyin. [svm-rs](https://github.com/alloy-rs/svm-rs):
```shell
cargo install svm-rs
svm install 0.8.19
```
İndirilen tüm kurulum parametreleri, derece `20`, `24` ve `26` kullanılmaktadır [config](https://github.com/scroll-tech/scroll-prover/tree/main/integration/configs).
Sadece 26 derece parametrelerini indirebildik, ancak bu parametrelerin küçültülmesi performansı etkileyebilir.
```shell
make download-setup -e degree=20
make download-setup -e degree=24
make download-setup -e degree=26
```
Veya indirmek için başka bir derece ve hedef dizin belirtin.

### Test
`make test-chunk-prove` ve `make test-e2e-prove`, scroll-prover'ın çok seviyeli devre kısıtlama sistemi için ana test girişleridir. Geliştiriciler, bu testlerin kodlarını 
okuyarak sistemin nasıl çalıştığını anlayabilirler.

Ve başka testler de var:
- `make test-inner-prove` birinci seviye devreyi test etmek için kullanılabilir.
- `make test-batch-prove` son iki seviyeyi test etmek için kullanılabilir.

### İkili Dosyalar
İkili dosyaları yerel olarak çalıştırmak için aşağıdaki komutu kullanabilirsiniz.
Parça kanıtı oluşturmak için zkevm kanıtlayıcısını çalıştırın
(çalışma dizini`./integration`)
```shell
# Params dosyası şu konumda bulunmalıdır:`./integration/params`.
cargo run --release --bin trace_prover -- --params=params --trace=tests/extra_traces/batch_34700/chunk_1236462/block_4176564.json
```
### Doğrulayıcı Sözleşme
Doğrulayıcı sözleşmenin hem YUL hem de bayt kodu, toplama testleri çalıştırıldığında oluşturulabilir.(`make test-e2e-prove`). Toplama testleri çalıştırıldıktan sonra, scroll-prover'ın integration klasöründe yeni bir klasör oluşturulur ve `integration/outputs/e2e_tests_*` gibi adlandırılır. Bu klasör aşağıdaki dosyaları içerir:
- Parça protokolü: `chunk_chunk_0.protocol`
- Parça VK: `vk_chunk_0.vkey`
- Yığın VK: `vk_batch_agg.vkey`
- Doğrulayıcı YUL kaynak kodu: `evm_verifier.yul`
- Doğrulayıcı bayt kodu: `evm_verifier.bin`

YUL kaynak kodu, parametreler, VK ve kanıt örneği numarası tarafından oluşturulur, [gen_evm_verifier function](https://github.com/scroll-tech/snark-verifier/blob/develop/snark-verifier-sdk/src/evm_api.rs#L121) snark-verifier içinde referans alabilirsiniz."

Doğrulayıcı bayt kodu, belirtilen parametrelerle komut satırında Solidity derleyicisi (yukarıda belirtilen 0.8.19 sürümü) kullanılarak YUL kaynak kodundan derlenir, 
[compile_yul function](https://github.com/scroll-tech/snark-verifier/blob/develop/snark-verifier/src/loader/evm/util.rs#L107) snark-verifier içinde referans alabilirsiniz.

## Lisans
Her ikisinden biri altında lisanslıdır
- Apache Lisansı, Versiyon 2.0, ([LICENSE-APACHE](LICENSE-APACHE) veya http://www.apache.org/licenses/LICENSE-2.0)
- MIT Lisansı ([LICENSE-MIT](LICENSE-MIT) veya http://opensource.org/licenses/MIT)


senin seçeneğin.














