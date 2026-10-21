# Sora Anime Mappings

Mapeamentos complementares de episódios do TMDB para o MyAnimeList, destinados ao SoraAnime.

Este repositório contém apenas correspondências adicionais. Não é uma cópia completa da base do [AniBridge](https://github.com/anibridge/anibridge-mappings) e não possui vínculo oficial com o projeto.

## Arquivo

O arquivo [`mappings.json`](./mappings.json) utiliza a estrutura de descritores e faixas de episódios do AniBridge:

```json
{
  "tmdb_show:46195:s1": {
    "mal:5081": {
      "1-12": "1-12"
    }
  }
}
```

- `tmdb_show:46195:s1`: série com ID 46195 no TMDB, temporada 1.
- `mal:5081`: anime com ID 5081 no MyAnimeList.
- `"1-12": "1-12"`: episódios 1 a 12 da temporada de origem correspondem aos episódios 1 a 12 no destino.
- `s0` representa a temporada de especiais do TMDB.

As correspondências são direcionais: uma entrada TMDB → MAL não define automaticamente o caminho inverso.

## Mapeamentos incluídos

### Bakemonogatari

| Origem no TMDB | Destino no MyAnimeList |
| --- | --- |
| Monogatari (46195), temporada 1, episódios 1–12 | Bakemonogatari (5081), episódios 1–12 |
| Monogatari (46195), especiais, episódios 2–4 | Bakemonogatari (5081), episódios 13–15 |

Referências: [TMDB](https://www.themoviedb.org/tv/46195), [MyAnimeList](https://myanimelist.net/anime/5081) e [AniList](https://anilist.co/anime/5081).

Estas entradas cobrem apenas Bakemonogatari, não as demais temporadas da franquia Monogatari.

## Uso planejado no SoraAnime

A integração deste complemento no app ainda precisa ser implementada. O comportamento previsto é:

1. Consultar primeiro a base oficial do AniBridge.
2. Quando não houver correspondência para o episódio, consultar este complemento.
3. Sincronizar somente se o mapeamento passar pelas validações do app; caso contrário, manter o episódio pendente.

Uma correspondência ambígua ou inválida na base oficial não deve ser substituída silenciosamente por este arquivo.

O app deverá acessar a URL pública Raw de `mappings.json`. Depois da integração, alterações neste arquivo poderão ser recebidas na renovação do cache, sem uma nova versão do APK.

## Como adicionar correspondências

1. Confirme os IDs do TMDB e do MAL e confira a numeração dos episódios nas duas plataformas.
2. Adicione a temporada de origem e o destino ao JSON, preservando as entradas existentes.
3. Para uma temporada já presente, acrescente o destino dentro do objeto existente. Não repita chaves JSON.
4. Informe as faixas exatas. Não deduza a equivalência apenas pelo nome do anime ou pelo número da temporada.
5. Atualize a documentação com o que foi adicionado e as referências usadas.
6. Valide a sintaxe antes de publicar:

```sh
python3 -m json.tool mappings.json > /dev/null
```

A validação acima verifica somente a sintaxe JSON, não a correção dos IDs ou das correspondências de episódios.

Não inclua tokens, credenciais ou dados pessoais neste repositório. Quando uma correção for incorporada e publicada na base oficial, confira a correspondência antes de remover a entrada complementar.
