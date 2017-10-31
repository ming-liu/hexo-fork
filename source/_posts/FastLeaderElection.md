---
title: FastLeaderElection
date: 2017-07-13 07:12:49
tags:
---

启动:

private void starter(QuorumPeer self, QuorumCnxManager manager) {
        this.self = self;
        proposedLeader = -1;
        proposedZxid = -1;

        sendqueue = new LinkedBlockingQueue<ToSend>();
        recvqueue = new LinkedBlockingQueue<Notification>();
        this.messenger = new Messenger(manager);
    }

org.apache.zookeeper.server.quorum.FastLeaderElection.ToSend    