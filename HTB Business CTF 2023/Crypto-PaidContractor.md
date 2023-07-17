# Desc Soalnya

Paid Contr-actor

After a lifetime of preparation, the moment has arrived to enlist in the esteemed military of the United Nations of Zenium as an expert in blockchain security. Before embarking on your duties, there is a small matter of paperwork that requires your attention.

# How-to

## Baca Kontraknya dulu
ini soal setupnya
untuk mensolve TARGET akan dicek status signed-nya
```Solidity

contract Setup {
    Contract public immutable TARGET;

    constructor() {
        TARGET = new Contract();
    }

    function isSolved() public view returns (bool) {
        return TARGET.signed();
    }
}

```

Contractnya ternyata hanya ada 1 fungsi yaitu signContract. jika dilihat cukup mengisi param dengan uint256 "1337" agar status signed berubah menjadi true
```Solidity

contract Contract {
    
    bool public signed;

    function signContract(uint256 signature) external {
        if (signature == 1337) {
            signed = true;
        }
    }

}
```

## Cara invoke pengerjaan

ini ternyata pakai foundry atau apapunlah.

```Foundry-Cast

cast send --privatekey <private-Key> <Contract Address> --rpc-url <URI> <Functionname(TypedataInput1,TypedataInput2)(TypedataOutput1,TypedataOutput2)> "Input1" "Input2"
```

	1.URI isinya adalah URI yang lengkap (Protocol://Address:port)
	2.Function Name samakan dengan fungsi kontrak yang ditarget

flagnya kebetulan ada di docker yang lain. gunakan netcat.

bignote: pada saat event belum bisa solved huhuhuhu


#easy #Blockchain
