SentencePiece
SentencePieceTrainer
Train()
Cú pháp:
spm.SentencePieceTrainer.Train(
     input=‘’ # bắt buộc phải là file
     sentence_interator=’iter()’ # dùng khi muốn chuyền list trực tiếp vào model
     model_prefix=
     model_type=
)
import sentencepiece as spm

spm.SentencePieceTrainer.Train(
    input='data.txt',             # file văn bản
    model_prefix='my_bpe',        # sinh ra my_bpe.model và my_bpe.vocab
    vocab_size=2000,              
    model_type='bpe'              # bpe / unigram / char / word
)
TrainerSpec {
  input: data.txt
  vocab_size: 2000
  model_type: BPE
}
Training finished. Output files:
 - my_bpe.model
 - my_bpe.vocab
SentencePieceProcessor()
import sentencepiece as spm

sp = spm.SentencePieceProcessor()
sp.Load("my_bpe.model")
True   # load thành công
.EncodeAsIds() & .EncodeAsPieces()
text = "xin chào mọi người"

print(sp.EncodeAsIds(text))
print(sp.EncodeAsPieces(text))
[58, 921, 117, 305, 92] 
['▁xin', '▁ch', 'ào', '▁m', 'ọi', '▁người']
.DecodeIds() & .DecodePieces()
ids = [58, 921, 117, 305]
pieces = ['▁xin', '▁ch', 'ào', '▁m']

print(sp.DecodeIds(ids))
print(sp.DecodePieces(pieces))
"xin chào m"
.encode()
print(sp.encode("học máy hiện đại", out_type=int))
print(sp.encode("học máy hiện đại", out_type=str))
[203, 88, 67, 450]
['▁học', '▁máy', '▁hiện', '▁đại']
sp.vocab_size()	kích thước vocab
sp.id_to_piece(id)	ID → subword
sp.piece_to_id("▁xin")	subword → ID
sp.is_unknown(id)	có phải token <unk>
sp.is_control(id)	token control
sp.get_piece_size()	số lượng piece
Bài tập
Demo bpe với data là list
import sentencepiece as spm

corpus = [
    "xin chào",
    "tôi tên là lê đức thắng",
    "bạn có khỏe không"
]

spm.SentencePieceTrainer.Train(
    sentence_iterator=iter(corpus),
    vocab_size=50,
    model_prefix="my_bpe",
    model_type="bpe"
)

sp = spm.SentencePieceProcessor()
sp.load("my_bpe.model")

print(sp.encode("xin chào các bạn", out_type=str))
