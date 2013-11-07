MODULES := pmap_xdr pmap_clnt rpc_clnt rpc_xdr pmap rpc_client rpc_server
ERLC = erlc
EBIN = ../ebin
OBJECTS := $(MODULES:%=$(EBIN)/%.beam)
ERLC_FLAGS = -Wall

all: $(OBJECTS)

clean:
	rm -f $(OBJECTS) nfs_svc.erl nfs_xdr.erl nfs.hrl

pmap.hrl: pmap.x
	erpcgen -a '[hrl]' pmap

pmap_clnt.erl: pmap.hrl pmap.x
	erpcgen -a '[clnt]' pmap

pmap_xdr.erl: pmap.x
	erpcgen -a '[xdr]' pmap

rpc.hrl: rpc.x
	erpcgen -a '[hrl]' rpc

rpc_xdr.erl: rpc.x
	erpcgen -a '[xdr]' rpc

rpc_clnt.erl:	rpc.hrl rpc.x
	erpcgen -a '[clnt]' rpc

$(EBIN)/rpc_server.beam: rpc.hrl
$(EBIN)/rpc_client.beam: rpc.hrl
$(EBIN)/pmap.beam: pmap.hrl

$(EBIN)/%.beam: %.erl
	$(ERLC) $(ERLC_FLAGS) -o $(EBIN) $<
