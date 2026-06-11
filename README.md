# rxdtestdata

Test data used by the NEURON `rxd` (Reaction-Diffusion) module.

This directory contains reference data files that the `rxd` test suite compares against. It is **not** intended to be edited manually.

## Regenerating Test Data

If the `rxd` tests are failing due to expected changes in output (e.g. after a code update), you can regenerate the reference data.

### New pytest-based tests (`test/rxd/testdata/test`)

```bash
cd /path/to/nrn

# Build the test mechanisms
nrnivmodl test/rxd

# Run the tests in "save" mode
PYTHONPATH=`pwd`/test/rxd:$PYTHONPATH \
    python -m pytest test/rxd --save=test/rxd/testdata/test
```

### Legacy rxdtests (`test/rxd/testdata/rxdtests`)

```bash
cd /path/to/nrn

python share/lib/python/neuron/rxdtests/run_all.py

cp -R share/lib/python/neuron/rxdtests/test_data/* test/rxd/testdata/rxdtests
```

## Comparing Data Sets

To compare a new set of test data against the version in `master`:

```bash
# Assuming:
#   current directory = new data
#   ../nrn             = master

test/rxd/compare_rxd_testdata_dirs.py test/rxd/testdata ../nrn/test/rxd/testdata
```

---

**Tip**: After regenerating data, commit the changes together with the code update that caused them. This keeps the test data in sync with the current behavior of the `rxd` module.
