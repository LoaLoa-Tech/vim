# vim
```
call plug#begin('~/.vim/plugged')

" find file
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
Plug 'junegunn/fzf.vim'

" This is javacomplete, an omni-completion script of JAVA language for vim 7.
Plug 'artur-shaik/vim-javacomplete2'

" file system explorer
Plug 'preservim/nerdtree'

" Asynchronous Lint Engine
Plug 'dense-analysis/ale'

" visual studio code: theme
Plug 'tomasiser/vim-code-dark'

" coc.nvim: True snippet and additional text editing support
Plug 'neoclide/coc.nvim', {'branch': 'release'}

" A Vim syntax highlighting plugin for JavaScript and Flow.js
Plug 'yuezk/vim-js'

" YouCompleteMe a code-completion engine for Vim
Plug 'Valloric/YouCompleteMe'

call plug#end()
" visual studio code theme
colorscheme codedark
let g:airline_theme = 'codedark'

" ===== ALE OPTION
let g:ale_linters = {
			\  'cs':['syntax', 'semantic', 'issues'],
			\  'python': ['pylint'],
			\  'java': ['eclipselsp']
			\ }


" ====== COC.NVIM OPTION
" coc.nvim: True snippet and additional text editing support
" - Setup Prettier
command! -nargs=0 Prettier :call CocAction('runCommand', 'prettier.formatFile')

" Use tab for trigger completion with characters ahead and navigate.
" NOTE: Use command ':verbose imap <tab>' to make sure tab is not mapped by
" other plugin before putting this into your config.
inoremap <silent><expr> <TAB>
			\ pumvisible() ? "\<C-n>" :
			\ <SID>check_back_space() ? "\<TAB>" :
			\ coc#refresh()
inoremap <expr><S-TAB> pumvisible() ? "\<C-p>" : "\<C-h>"

function! s:check_back_space() abort
	let col = col('.') - 1
	return !col || getline('.')[col - 1]  =~# '\s'
endfunction

" Use <c-space> to trigger completion.
if has('nvim')
	inoremap <silent><expr> <c-space> coc#refresh()
else
	inoremap <silent><expr> <c-@> coc#refresh()
endif

" Make <CR> auto-select the first completion item and notify coc.nvim to
" format on enter, <cr> could be remapped by other vim plugin
inoremap <silent><expr> <cr> pumvisible() ? coc#_select_confirm()
			\: "\<C-g>u\<CR>\<c-r>=coc#on_enter()\<CR>"
" Use K to show documentation in preview window.
nnoremap <silent> K :call <SID>show_documentation()<CR>

function! s:show_documentation()
	if (index(['vim','help'], &filetype) >= 0)
		execute 'h '.expand('<cword>')
	elseif (coc#rpc#ready())
		call CocActionAsync('doHover')
	else
		execute '!' . &keywordprg . " " . expand('<cword>')
	endif
endfunction



" ====== vim-javacomplete2 OPTION 
autocmd FileType java setlocal omnifunc=javacomplete#Complete
" - add all missing imports with F6:
nmap <F6> <Plug>(JavaComplete-Imports-AddMissing)
imap <F6> <Plug>(JavaComplete-Imports-AddMissing)
" remove all unused imports with F7:
nmap <F7> <Plug>(JavaComplete-Imports-RemoveUnused)
imap <F7> <Plug>(JavaComplete-Imports-RemoveUnused)



" ===== pangloss/vim-javascript OPTION
" Enables syntax highlighting for JSDocs.
let g:javascript_plugin_jsdoc = 1
" Enables some additional syntax highlighting for NGDocs. Requires JSDoc plugin to be enabled as well.
let g:javascript_plugin_ngdoc = 1
" Enables syntax highlighting for Flow.
let g:javascript_plugin_flow = 1
" Concealing Characters
let g:javascript_conceal_function             = "ƒ"
let g:javascript_conceal_null                 = "ø"
let g:javascript_conceal_this                 = "@"
let g:javascript_conceal_return               = "⇚"
let g:javascript_conceal_undefined            = "¿"
let g:javascript_conceal_NaN                  = "ℕ"
let g:javascript_conceal_prototype            = "¶"
let g:javascript_conceal_static               = "•"
let g:javascript_conceal_super                = "Ω"
let g:javascript_conceal_arrow_function       = "⇒"
set conceallevel=1




" ===== CUSTOM OPTION
" How can I open a NERDTree automatically when vim starts up if no files were specified?
autocmd StdinReadPre * let s:std_in=1
autocmd VimEnter * if argc() == 0 && !exists("s:std_in") | NERDTree | endif
" How can I open NERDTree automatically when vim starts up on opening a directory?
autocmd StdinReadPre * let s:std_in=1
autocmd VimEnter * if argc() == 1 && isdirectory(argv()[0]) && !exists("s:std_in") | exe 'NERDTree' argv()[0] | wincmd p | ene | exe 'cd '.argv()[0] | endif
" open NERDTree with Ctrl+n
map <C-n> :NERDTreeToggle<CR>
" format and save
map <C-s> :Prettier <CR>:w<CR>
" Fzf map
map <C-f> :Files <CR>
" format ejs
au BufNewFile,BufRead *.ejs set filetype=html
set number
set encoding=utf-8
let java_highlight_functions = 1
```
