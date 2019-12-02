# DICOM De-Identify

A small and configurable Scala library to de-identify DICOM files according to Supp. 142.

## Using

Add as as a dependency to your project. Start coding.

```scala
de.stereotypez.Deidentify

val din = new DicomInputStream(new File("yourfile.dcm"))
val fmi = din.readFileMetaInformation()
val att = din.readDataset(-1, -1)
din.close()

// runs with side effects (will modify 'att')
Deidentify()
  .keep(Tag.PatientSex, Tag.PatientSize, Tag.PatientWeight)
  .withOptions(RetainLongModifDatesOption)
  .execute(att)

// write to new DICOM file
val dout = new DicomOutputStream(new File("de-identified.dcm"))
dout.writeDataset(fmi, att)
dout.close()

```

## Running the tests

```bash
mvn test
```

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* https://github.com/neurosnap/dicom_codify/ for parsing this horrible  

