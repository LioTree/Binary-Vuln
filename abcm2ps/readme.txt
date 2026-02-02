### Vulnerability 1
Vulnerability Type: Global Buffer Overflow
Vendor: https://salsa.debian.org/debian/abcm2ps.git             
Affected product: abcm2ps 8.14.17-3

Attack type:        Context-dependent
Impact:             Denial of Service
Affected component: glyph_out() in glyph.c
Attack vector:      Crafted input file with invalid UTF-8 sequences

Description:        A global buffer overflow vulnerability exists in the glyph_out() function in glyph.c. The function does not properly validate UTF-8 byte sequences before using them as array indices. When processing crafted input files with invalid UTF-8 sequences (such as bytes 0xC0-0xC1 which are not valid in UTF-8), the function calculates negative or out-of-range array indices and accesses the utf_1[], c2[], c3[], c4[], and c5[] global arrays out of bounds, leading to a global buffer overflow.

Trace:
  id:000001,sig:06,src:000000,time:177030,execs:46963,op:havoc,rep:7: [READ,global-buffer-overflow]@main->treat_abc_file->treat_file->frontend->txt_add_eos->abc_parse->do_tune->gen_ly->generate->output_music->delayed_output->draw_sym_near->draw_all_lyrics->draw_lyrics->draw_lyric_line->put_str->str_out->str_ft_out->glyph_out
  id:000000,sig:06,src:000000,time:171523,execs:45461,op:havoc,rep:5: [READ,global-buffer-overflow]@main->treat_abc_file->treat_file->frontend->abc_eof->do_tune->get_info->write_heading->write_title->put_str->str_out->str_ft_out->glyph_out
  id:000003,sig:06,src:000002,time:387331,execs:102899,op:quick,pos:1257,val:+2: [READ,global-buffer-overflow]@main->treat_abc_file->treat_file->frontend->abc_eof->do_tune->gen_ly->put_words->put_wline->put_str->str_out->str_ft_out->glyph_out
  id:000007,sig:06,src:000002,time:435918,execs:115338,op:havoc,rep:2: [READ,global-buffer-overflow]@main->treat_abc_file->treat_file->frontend->abc_eof->do_tune->gen_ly->generate->output_music->delayed_output->draw_sym_near->draw_deco_staff->draw_gchord->str_out->str_ft_out->glyph_out


### Vulnerability 2
Vulnerability Type: Global Buffer Overflow
Vendor: https://salsa.debian.org/debian/abcm2ps.git
Affected product: abcm2ps 8.14.17-3

Attack type:        Context-dependent
Impact:             Denial of Service
Affected component: draw_rest() in draw.c
Attack vector:      Crafted input file with negative note position

Description:        A global buffer overflow vulnerability exists in the draw_rest() function in draw.c. The function calculates an array index j as y/6 where y can be negative. The code then accesses stafflines[j] without checking if j is negative, causing an out-of-bounds read before the start of the stafflines array.

Trace:
  id:000002,sig:06,src:000002,time:383670,execs:102043,op:quick,pos:513,val:+2: [READ,global-buffer-overflow]@main->treat_abc_file->treat_file->frontend->abc_eof->do_tune->gen_ly->generate->output_music->draw_all_symb->draw_symbols->draw_rest