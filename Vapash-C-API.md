---
name: Vapash C API
category: 
---

This is just a documentation of the request of the C API described in [this PR](https://github.com/vaporyco/vapash/pull/11).

```c
typedef int(*Callback)(unsigned);
typedef /*...*/ vapash_light_t;
typedef /*...*/ vapash_full_t;
typedef struct vapash_h256 { uint8_t b[32]; } vapash_h256_t;
typedef struct vapash_result { vapash_h256_t value; vapash_h256_t hixhash; } vapash_result_t;

vapash_light_t vapash_light_new(unsigned number);
vapash_result_t vapash_light_compute(vapash_light_t light, vapash_h256_t header_hash, uint64_t nonce);
void vapash_light_delete(vapash_light_t light);

vapash_full_t vapash_full_new(vapash_light_t light, CallBack c);
uint64_t vapash_full_dag_size(vapash_full_t full);
void const* vapash_full_dag(vapash_full_t full);
vapash_result_t vapash_full_compute(vapash_full_t full, vapash_h256_t header_hash, uint64_t nonce);
void vapash_full_delete(vapash_full_t full);
```

non-zero return from Callback means "cancel DAG creation" - this should cause an immediate return of `vapash_full_new` with 0.

an object of type `vapash_full_t` may be tested for validity with != 0

### Example usage:
```c
int callback(unsigned _progress)
{
  printf("\rGenerating DAG. %d%% done...", _progress);
  return 0;
}
void main()
{
  vapash_light_t light;
  vapash_h256_t seed;
  // TODO: populate p, seed, light
  vapash_full_t dag = vapash_full_new(light, seed, &callback);
  if (!dag)
  {
    printf("Failed generating DAG :-(\n");
    exit(-1);
  }
  printf("DAG Generated OK!\n");

  vapash_h256_t headerHash;
  // TODO: populate headerHash
  uint64_t nonce = time(0);
  vapash_result ret;
  for (; !isWinner(ret); nonce++)
    ret = vapash_full_compute(dag, headerHash, nonce);
  printf("Got winner! nonce is %d\n", nonce);
  vapash_full_delete(dag);
}
```